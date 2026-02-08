# MPFR 実装漏れ関数リスト

このファイルは、plan.mdで言及されているがまだ実装されていない関数のリストです。

## ✅ 実装完了！

**すべての関数の実装とテストが完了しました。**

- 実装日: 2026年2月8日
- 実装した関数数: 43関数
- テスト追加: 10個の新しいテスト関数
- テスト結果: すべてパス (ERROR SUMMARY: 0 errors)
- メモリリーク: なし (definitely lost: 0 bytes)

### 実装統計

- mpfr.fix: 847行 → 1,327行 (+480行)
- mpfr-test.fix: 386行 → 579行 (+193行)
- 総関数数: 99個 (内部関数含む)

### フェーズ別実装内容

**Phase 1: 基本的でよく使われる関数 (12関数)**
- ✅ div_2ui, div_2si - ビットシフト除算
- ✅ exp2, exp10, expm1, log1p - 拡張指数・対数関数
- ✅ ceil, floor, round, trunc - 整数化関数
- ✅ min, max - 最小・最大値

**Phase 2: 重要な数学関数 (6関数)**
- ✅ fma - fused multiply-add
- ✅ hypot - ユークリッド距離
- ✅ agm - 算術幾何平均
- ✅ fac_ui - 階乗
- ✅ fmod, remainder - 剰余演算

**Phase 3: 追加の三角関数 (6関数)**
- ✅ sec, csc, cot - 正割、余割、余接
- ✅ sech, csch, coth - 双曲線正割、余割、余接

**Phase 4: 高度な特殊関数 (11関数)**
- ✅ zeta, zeta_ui - リーマンゼータ関数
- ✅ beta, digamma - ベータ関数、ディガンマ関数
- ✅ j0, j1, jn, y0, y1, yn - ベッセル関数
- ✅ ai - エアリー関数

**Phase 5: ユーティリティ関数と定数 (7関数)**
- ✅ signbit, copysign, setsign - 符号操作
- ✅ nexttoward, nextabove, nextbelow - 隣接値操作
- ✅ const_catalan - カタラン定数

### テストカバレッジ

すべての新しい関数に対してテストを追加しました:
- test_bit_shift_division - ビットシフト除算のテスト
- test_exponential_extended - 拡張指数・対数関数のテスト
- test_integer_functions - 整数化関数のテスト
- test_minmax - 最小・最大値のテスト
- test_advanced_math - 高度な数学関数のテスト
- test_additional_trig - 追加の三角関数のテスト
- test_zeta_beta - ゼータ・ベータ関数のテスト
- test_bessel - ベッセル関数のテスト
- test_utilities - ユーティリティ関数のテスト

## 実装済み関数の確認

現在実装済みの関数:
- 基本演算: add, sub, mul, div, neg, abs
- べき乗・根: sqr, sqrt, rec_sqrt, cbrt, rootn_ui, pow, pow_ui, pow_si
- ビットシフト乗算: mul_2ui, mul_2si
- 指数・対数: exp, log, log2, log10
- 三角関数: sin, cos, tan, asin, acos, atan, atan2
- 双曲線関数: sinh, cosh, tanh, asinh, acosh, atanh
- 特殊関数: gamma, lngamma, erf, erfc
- 定数: const_pi, const_log2, const_euler
- 比較: cmp, equal, less, lesseq
- 述語: is_nan, is_inf, is_number, is_zero, sgn

## ✅ すべて実装完了した関数リスト

### Category 1: ビットシフト除算 (2関数) ✅
- [x] `div_2ui : U64 -> MPFR -> MPFR` - 2^nで除算 (符号なし)
- [x] `div_2si : I64 -> MPFR -> MPFR` - 2^nで除算 (符号あり)

### Category 2: 指数・対数の追加関数 (4関数) ✅
- [x] `exp2 : MPFR -> MPFR` - 2^x
- [x] `exp10 : MPFR -> MPFR` - 10^x
- [x] `expm1 : MPFR -> MPFR` - exp(x)-1 (小さいxで高精度)
- [x] `log1p : MPFR -> MPFR` - log(1+x) (小さいxで高精度)

### Category 3: 整数化関数 (4関数) ✅
- [x] `ceil : MPFR -> MPFR` - 天井関数（切り上げ）
- [x] `floor : MPFR -> MPFR` - 床関数（切り捨て）
- [x] `round : MPFR -> MPFR` - 最近接整数への丸め
- [x] `trunc : MPFR -> MPFR` - ゼロ方向への切り捨て

### Category 4: 最小・最大 (2関数) ✅
- [x] `min : MPFR -> MPFR -> MPFR` - 2つの値の最小値
- [x] `max : MPFR -> MPFR -> MPFR` - 2つの値の最大値

### Category 5: その他の重要な数学関数 (4関数) ✅
- [x] `fma : MPFR -> MPFR -> MPFR -> MPFR` - fused multiply-add (x*y+z)
- [x] `hypot : MPFR -> MPFR -> MPFR` - sqrt(x²+y²)
- [x] `agm : MPFR -> MPFR -> MPFR` - 算術幾何平均
- [x] `fac_ui : U64 -> Precision -> MPFR` - 階乗 (n!)

### Category 6: 剰余関数 (2関数) ✅
- [x] `fmod : MPFR -> MPFR -> MPFR` - 浮動小数点剰余
- [x] `remainder : MPFR -> MPFR -> MPFR` - IEEE remainder

### Category 7: その他の三角関数 (6関数) ✅
- [x] `sec : MPFR -> MPFR` - 正割 sec(x) = 1/cos(x)
- [x] `csc : MPFR -> MPFR` - 余割 csc(x) = 1/sin(x)
- [x] `cot : MPFR -> MPFR` - 余接 cot(x) = 1/tan(x)
- [x] `sech : MPFR -> MPFR` - 双曲線正割 sech(x) = 1/cosh(x)
- [x] `csch : MPFR -> MPFR` - 双曲線余割 csch(x) = 1/sinh(x)
- [x] `coth : MPFR -> MPFR` - 双曲線余接 coth(x) = 1/tanh(x)

### Category 8: ゼータ・ベータ・ディガンマ関数 (4関数) ✅
- [x] `zeta : MPFR -> MPFR` - リーマンゼータ関数
- [x] `zeta_ui : U64 -> Precision -> MPFR` - 整数引数のゼータ関数
- [x] `beta : MPFR -> MPFR -> MPFR` - ベータ関数
- [x] `digamma : MPFR -> MPFR` - ディガンマ関数 (ψ関数)

### Category 9: ベッセル関数 (6関数) ✅
- [x] `j0 : MPFR -> MPFR` - 第一種ベッセル関数 J0
- [x] `j1 : MPFR -> MPFR` - 第一種ベッセル関数 J1
- [x] `jn : I64 -> MPFR -> MPFR` - 第一種ベッセル関数 Jn
- [x] `y0 : MPFR -> MPFR` - 第二種ベッセル関数 Y0
- [x] `y1 : MPFR -> MPFR` - 第二種ベッセル関数 Y1
- [x] `yn : I64 -> MPFR -> MPFR` - 第二種ベッセル関数 Yn

### Category 10: その他の特殊関数 (1関数) ✅
- [x] `ai : MPFR -> MPFR` - エアリー関数

### Category 11: 符号・ビット操作 (3関数) ✅
- [x] `signbit : MPFR -> Bool` - 符号ビットのテスト
- [x] `copysign : MPFR -> MPFR -> MPFR` - 符号のコピー
- [x] `setsign : Bool -> MPFR -> MPFR` - 符号の設定

### Category 12: 隣接値操作 (3関数) ✅
- [x] `nexttoward : MPFR -> MPFR` - 指定方向の隣接浮動小数点値
- [x] `nextabove : MPFR -> MPFR` - より大きい隣接値
- [x] `nextbelow : MPFR -> MPFR` - より小さい隣接値

### Category 13: 追加の数学定数 (1関数) ✅
- [x] `const_catalan : Precision -> MPFR` - カタラン定数

## 実装の優先順位

### Phase 1: 基本的でよく使われる関数 (12関数)
Category 1, 2, 3, 4

### Phase 2: 重要な数学関数 (6関数)
Category 5, 6

### Phase 3: 追加の三角関数 (6関数)
Category 7

### Phase 4: 高度な特殊関数 (12関数)
Category 8, 9, 10

### Phase 5: ユーティリティ関数と定数 (7関数)
Category 11, 12, 13

**合計: 43関数**

## 実装方針

- すべて`_unary_op`, `_binary_op`パターンまたは類似のパターンを使用
- デフォルト丸めモードはRNDN
- 精度の扱いは既存の関数と同様に
