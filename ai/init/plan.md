# MPFR Fix Wrapper プロジェクト計画書

## 1. プロジェクト概要

GNU MPFRライブラリ (Multiple Precision Floating-Point Reliable) をFixでラップする。MPFRは任意精度の浮動小数点演算を提供し、GMPライブラリをベースとしている。

MPFRの主な特徴:
- 任意のビット精度（変数ごとに設定可能）
- IEEE 754の丸めモード（RNDN, RNDD, RNDU, RNDZ）とaway-from-zero (RNDA) をサポート
- 正確な計算結果の保証

## 2. グローバル状態問題と解決策

### 2.1 問題

MPFRには関数型言語と相性の悪いグローバル状態があります：

1. **デフォルト精度**: `mpfr_set_default_prec`/`mpfr_get_default_prec` により、グローバルなデフォルト精度を設定できる。`mpfr_init`はこの値を使用する。

2. **指数範囲**: グローバルまたはスレッドローカルな指数範囲（ただし、これは通常変更する必要がない）

3. **例外フラグ**: グローバルまたはスレッドローカルな例外フラグ（Underflow, Overflow等）

4. **デフォルト丸めモード**: グローバルなデフォルト丸めモード（ただし、ほとんどの関数は丸めモードを引数として受け取る）

### 2.2 解決策

#### 精度の扱い

**方針**: グローバルなデフォルト精度を使用せず、**常に明示的に精度を指定する**。

- すべてのコンストラクタで精度を明示的に要求する
- `mpfr_init`ではなく`mpfr_init2(prec)`を使用する
- GMP.Zの`MPZ`型同様、Fixらしいインターフェースを提供するため、演算結果の精度は以下のルールに従う：
  - 単項演算: 入力と同じ精度
  - 二項演算: 両オペランドの最大精度
  - このルールにより、ユーザーは精度を明示的に管理できる

#### 丸めモード

**方針**: 各演算関数で丸めモードを指定できるようにしつつ、デフォルトはRNDN（最近接丸め）とする。

- `RoundMode` enumを定義
- 基本的な演算（Add, Sub, Mul, Div等のトレイト実装）はデフォルトでRNDNを使用
- 丸めモードを明示的に指定したい場合は、専用の関数を使用する（例：`add_with_rnd`）

#### 例外フラグ

**方針**: このラッパーでは例外フラグを基本的にサポートしない。

- MPFRの例外フラグは主にデバッグや特殊なケースのために使用される
- Fixの関数型スタイルでは、例外情報は戻り値（Option, Result等）として返すべき
- 必要に応じて、将来的に例外クエリ関数をラップすることは可能

#### 指数範囲

**方針**: デフォルトの指数範囲を使用し、通常は変更しない。

- MPFRのデフォルト指数範囲は非常に広い（約±10^18乗）
- 特殊な用途でない限り変更する必要はない
- 将来的に必要になった場合にのみ、指数範囲の設定関数を追加する

## 3. 型設計

### 3.1 MPFR型

```fix
type MPFR = unbox struct { _0 : Destructor MPFRHandle };
```

- GMP.ZのMPZ型と同様のパターン
- `Destructor`を使用した自動メモリ管理
- `_borrow`, `_mutate`パターンによるcopy-on-write最適化

### 3.2 RoundMode型

```fix
type RoundMode = unbox union {
    rndn : (),  // Round to Nearest (ties to even)
    rndz : (),  // Round toward Zero
    rndu : (),  // Round toward positive infinity
    rndd : (),  // Round toward negative infinity
    rnda : (),  // Round Away from zero
};
```

- 各丸めモードをC定数にマッピング
- デフォルトはRNDN

### 3.3 Precision型

```fix
type Precision = I64;
```

- 精度はビット単位
- I64で十分（現実的な精度は数百万ビット程度まで）
- 型エイリアスにより、コードの可読性と意図が明確になる

## 4. コンストラクタ

### 4.1 基本コンストラクタ

- `mpfr : Precision -> I64 -> MPFR` - I64から作成
- `mpfr_f64 : Precision -> F64 -> MPFR` - F64から作成
- `mpfr_str : Precision -> String -> I64 -> Option MPFR` - 文字列から作成（基数指定）

### 4.2 GMP型からの変換

- `from_mpz : Precision -> MPZ -> MPFR` - MPZから作成
- `from_mpq : Precision -> MPQ -> MPFR` - MPQから作成

### 4.3 特殊値

- `zero : Precision -> MPFR` - ゼロ
- `nan : Precision -> MPFR` - NaN
- `inf : Precision -> MPFR` - 正の無限大
- `neg_inf : Precision -> MPFR` - 負の無限大

## 5. トレイト実装

### 5.1 Zero トレイト

```fix
impl MPFR : Zero {
    zero = zero(53);  // 53ビット精度（F64相当）をデフォルトとする
}
```

### 5.2 算術演算トレイト

- `Add`, `Sub`, `Mul`, `Div` - 丸めモードはRNDN、精度は両オペランドの最大値
- `Neg` - 符号反転（正確な演算）

### 5.3 比較トレイト

- `Eq` - `mpfr_equal_p`を使用
- `LessThan` - `mpfr_less_p`を使用
- `LessThanOrEq` - `mpfr_lessequal_p`を使用

### 5.4 変換トレイト

- `ToString` - `mpfr_get_str`を使用し、適切な形式で文字列化
- `FromString` - `init_set_str`のラッパー

### 5.5 その他のトレイト

- `Hash` - 値をバイト列としてハッシュ化（要検討）

## 6. 関数ラッピング戦略

### 6.1 命名規則

- GMP.Zと同様に、`mpfr_`プレフィックスを削除し、`MPFR::`名前空間に配置
- 例: `mpfr_add` → `MPFR::add`
- Fix命名規則に従い、一部の関数は名前を調整（例: `mpfr_2fac_ui` → `MPFR::fac2_ui`）

### 6.2 引数順序

- Fixらしいインターフェースのため、引数順序を調整
- 例: `x.add(y)` のように自然に書けるようにする
- 出力引数は返り値として扱う

### 6.3 関数カテゴリ

以下のカテゴリの関数をラップする：

#### 初期化・代入関数
- `init2`, `clear` (内部使用)
- `set`, `set_si`, `set_ui`, `set_d`, `set_z`, `set_q`, `set_str` 等

#### 変換関数
- `get_si`, `get_ui`, `get_d`, `get_z`, `get_q`, `get_str` 等

#### 算術演算
- `add`, `sub`, `mul`, `div`, `sqr`, `sqrt`, `cbrt`, `root`, `pow` 等
- `neg`, `abs` 等

#### 比較関数
- `cmp`, `cmp_si`, `cmp_ui`, `cmp_d`, `cmp_z`, `cmp_q`
- `less_p`, `equal_p`, `lessgreater_p`, `unordered_p` 等

#### 数学関数
- 三角関数: `sin`, `cos`, `tan`, `asin`, `acos`, `atan`, `atan2`
- 双曲線関数: `sinh`, `cosh`, `tanh`, `asinh`, `acosh`, `atanh`
- 指数・対数: `exp`, `exp2`, `exp10`, `log`, `log2`, `log10`
- ガンマ・ゼータ関数: `gamma`, `lngamma`, `zeta`, `erf`, `erfc`
- ベッセル関数: `j0`, `j1`, `jn`, `y0`, `y1`, `yn`
- その他: `fac_ui`, `fma`, `hypot`, `agm`, `const_pi`, `const_euler` 等

#### 特殊関数群
- 整数関数: `ceil`, `floor`, `round`, `trunc`, `rint`
- 剰余: `fmod`, `remainder`
- 最小・最大: `min`, `max`
- その他: `signbit`, `copysign`, `nexttoward`, `nextabove`, `nextbelow`

#### 述語関数
- `nan_p`, `inf_p`, `number_p`, `zero_p`, `regular_p`, `sgn`

### 6.4 関数の実装パターン

GMP.Zと同様に、`_unary_op`, `_binary_op`等のヘルパー関数を使用し、copy-on-write最適化を実現する。

```fix
add : MPFR -> MPFR -> MPFR;
add = |lhs, rhs| (
    let prec = max(lhs.get_prec, rhs.get_prec);
    let rnd = RoundMode::rndn().to_c_rnd;
    _binary_op_with_prec(prec, rnd, |out_ptr, lhs_ptr, rhs_ptr|
        FFI_CALL_IO[CInt mpfr_add(Ptr, Ptr, Ptr, CInt), 
                    out_ptr, lhs_ptr, rhs_ptr, rnd]
    , lhs, rhs).@0
);
```

## 7. テスト戦略

### 7.1 テストファイル構成

- `mpfr.fix` - MPFR型と関数の定義
- `mpfr-test.fix` - テストコード
- GMP.Zと同様に、ほぼすべての関数を実際に呼び出すテストを作成

### 7.2 テスト内容

1. **基本操作テスト**
   - 初期化、代入、取得
   - メモリリーク検証（valgrindでチェック）

2. **算術演算テスト**
   - 基本演算（+, -, *, /）
   - べき乗、平方根等
   - 丸めモードによる結果の違いを確認

3. **精度テスト**
   - 異なる精度での計算結果を検証
   - 精度が結果に与える影響を確認

4. **数学関数テスト**
   - 三角関数、指数・対数関数等
   - 既知の値との比較（例: pi, e）

5. **特殊値テスト**
   - NaN, Inf, 0の処理
   - 符号付きゼロ

6. **変換テスト**
   - I64, F64, String, MPZ, MPQとの相互変換

7. **比較テスト**
   - 等価性、大小比較

## 8. プロジェクト構成

```
/home/maruyama/fixlang-projs/gmpfr/
├── fixproj.toml           # プロジェクト設定
├── mpfr.fix               # MPFR型と関数
├── mpfr-test.fix          # テストコード
├── LICENSE                # ライセンス
├── README.md              # プロジェクト説明
├── ai/                    # 参考資料（実装時の参照用）
│   ├── instruction.md     # プロジェクトの指示書
│   ├── plan.md            # このファイル
│   ├── mpfr.html          # MPFR 4.1.0のドキュメント
│   ├── gmp/               # GMP Fixラッパーの参考実装
│   └── fixlang/           # Fix言語のドキュメント
└── docs/                  # fix docsで生成
    └── MPFR.md
```

**注記**: `ai/`フォルダはこのプロジェクトを実装するAIが参考にできるドキュメントやコードを含んでいます。

## 9. 実装の優先順位

1. **フェーズ1**: 基本構造
   - 型定義 (MPFR, RoundMode)
   - 基本コンストラクタ
   - メモリ管理（_borrow, _mutate）
   - 基本的なテスト

2. **フェーズ2**: 基本演算
   - トレイト実装（Zero, Add, Sub, Mul, Div, Neg）
   - 比較演算（Eq, LessThan）
   - ToString実装
   - テスト追加

3. **フェーズ3**: 数学関数
   - 算術演算（sqr, sqrt, pow等）
   - 三角関数、指数・対数関数
   - テスト追加

4. **フェーズ4**: 詳細機能
   - 変換関数（MPZ, MPQ等）
   - 特殊関数群
   - 述語関数
   - 包括的なテスト

5. **フェーズ5**: ドキュメント生成
   - `fix docs`でドキュメント生成
   - README.mdの充実

## 10. 特記事項

### 10.1 GMP依存

- MPFRはGMPに依存している
- このプロジェクトは`gmp-fix`パッケージに依存する
- `GMP.Z::MPZ`型と`GMP.Q::MPQ`型を使用する関数（`mpfr_set_z`, `mpfr_get_z`, `mpfr_set_q`, `mpfr_get_q`等）をラップする
- フェーズ4でGMP型との変換関数を実装する

### 10.3 Stdの自動インポートとキャスト関数

#### Stdの自動インポート
- Stdモジュールのエンティティは自動的にインポートされるため、明示的な`import Std::{...}`は不要
- 開発中は明示的なimportを省略し、実装完了後に`fix edit explicit-import`コマンドで明示的インポートスタイルに変換可能

#### キャスト関数の使用
- **重要**: 新しいFix言語では、`to_I64`, `to_CInt`のような古いキャスト関数ではなく、`i64`, `c_int`のような新しいキャスト関数を使用する
- 例:
  - `to_I64` → `i64` (例: `val.i64`)
  - `to_CInt` → `c_int` (例: `32.c_int`)
  - `to_CLong` → `c_long` (例: `val.c_long`)
  - `to_CUnsignedLong` → `c_unsigned_long` (例: `val.c_unsigned_long`)
  - `to_CDouble` → `c_double` (例: `val.c_double`)
- これらのキャスト関数はStdで定義されており、自動インポートで利用可能
- ai/gmp内のコードは古い書き方を使用している場合があるため、参考にする際は注意が必要

### 10.2 fixproj.tomlの設定

```toml
[general]
name = "mpfr-fix"
version = "0.1.0"

[build]
files = ["mpfr.fix"]
dynamic_links = ["mpfr", "gmp"]

[build.test]
files = ["mpfr-test.fix"]
memcheck = true

[[dependencies]]
name = "gmp-fix"
version = "0.6.4"
```

### 10.4 パフォーマンス

- GMP.Zと同様に、copy-on-write最適化によりメモリコピーを最小化
- `unsafe_is_unique`を使用した最適化

### 10.5 今後の拡張可能性

- スレッドセーフ対応（MPFRはスレッドローカルストレージをサポート）
- カスタムメモリアロケータ対応
- より高度な丸めモード制御
- 例外フラグのサポート（必要に応じて）
