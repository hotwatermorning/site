# laguerre
* cmath[meta header]
* function[meta id-type]
* std[meta namespace]
* [mathjax enable]
* cpp17[meta cpp]

```cpp
namespace std {
float laguerref(unsigned n, float x);
double laguerre(unsigned n, double x);
long double laguerrel(unsigned n, long double x);
}
```

## 概要
ラゲール多項式 (Laguerre polynomials) を求める。

## 戻り値
引数 `n`, `x` のラゲール多項式
$$ L_n(x) = \frac{e^x}{n!} \frac{\mathrm{d}^n}{\mathrm{d}x^n} (x^n e^{-x}) \text{ for } x \ge 0 $$
を返す。


## 備考
`n >= 128` の場合、この関数の呼び出しの効果は実装定義である。


## 例
```cpp
#include <cmath>
#include <iostream>

int main() {
  std::cout << "laguerre(0, 0) = " << std::laguerre(0, 0) << std::endl; // L0 = 1
  std::cout << "laguerre(1, 1) = " << std::laguerre(1, 1) << std::endl; // L1 = -x + 1
  std::cout << "laguerre(2, 2) = " << std::laguerre(2, 2) << std::endl; // L2 = x^2 / 2 - 2x + 1
}
```
* std::laguerre[color ff0000]

### 出力例
```
laguerre(0, 0) = 1
laguerre(1, 1) = 0
laguerre(2, 2) = -1
```


## バージョン
### 言語
- C++17

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 7.1.0
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): ??

### 備考
#### GCC (libstdc++)
GCC 7.1.0–8.0.0 では定義域エラーが発生したときに [`std::domain_error`](/reference/stdexcept.md) を送出する。


## 参照
- [N3060 JTC1.22.29124 Programming Language C++ — Special Math Functions](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2010/n3060.pdf)
- [WG21 P0226R1 Mathematical Special Functions for C++17, v5](https://isocpp.org/files/papers/P0226R1.pdf)
- [ISO/IEC 29124:2010 Information technology -- Programming languages, their environments and system software interfaces -- Extensions to the C++ Library to support mathematical special functions](https://www.iso.org/standard/50511.html)


## 実装例
$$ L_n(x) = \sum_{j=0}^n {}_n\mathrm{C}_j \frac{(-1)^j}{j!} x^j $$

あるいは漸化式
$$ L_{n}(x) = \frac{(2n - 1 - x) L_{n-1}(x) - (n-1) L_{n-2}(x)}{n - 2}; L_0(x) = 1, L_1(x) = -x + 1 $$
を用いる。