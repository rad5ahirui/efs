# 1 記号列操作用言語
## 問題1.3.1.
(a), (b), (c), (e)が手続きである.
(d)は原子文 `PARTA(y, x)` が代入の位置に来ているが,
`PARTA` は予約識別子のリストにはないため, 手続きではない.

## 問題1.3.2.
(a)-(e).

## 問題1.4.1.
### (a)
```
SHORTER(2):
    SHORTER('', 0);
    SHORTER('', 1);
    SHORTER(x, y)->CON(y, 0, z)->SHORTER(x, z);
    SHORTER(x, y)->CON(y, 1, z)->SHORTER(x, z);
    SHORTER(x, y)->CON(x, 0, z)->CON(y, 0, w)->SHORTER(z, w);
    SHORTER(x, y)->CON(x, 0, z)->CON(y, 1, w)->SHORTER(z, w);
    SHORTER(x, y)->CON(x, 1, z)->CON(y, 0, w)->SHORTER(z, w);
    SHORTER(x, y)->CON(x, 1, z)->CON(y, 1, w)->SHORTER(z, w).
```

### (b)
```
SHORTER('', 1)
SHORTER('', 1)->CON('', 0, 0)->CON(1, 0, 10)->SHORTER(0, 10)
SHORTER(0, 10)->CON(0, 1, 01)->CON(10, 1, 101)->SHORTER(01, 101)
```

言っていることがよくわからないので, これ以降自信なし.

## 問題1.4.2.
```
SHORTER('', 0)
CON('', 1, 1)
CON(0, 0, 00)
SHORTER('', 0)->CON('', 1, 1)->CON(0, 0, 00)->SHORTER(1, 00)
SHORTER(1, 00)
CON(00, 0, 000)
SHORTER(1, 00)->CON(00, 0, 000)->SHORTER(1, 000)
SHORTER(1, 000)
```

## 問題1.4.3.
### <0, 1>
```
CON('', 0, 0)
CON('', 1, 1)
CON('', 0, 0)->CON('', 1, 1)->SUC(0, 1)
SUC(0, 1)
```

### <1, 10>
```
SUC(1, 10)
```

### <10, 11>
```
CON(1, 0, 10)
CON(1, 1, 11)
CON(1, 0, 10)->CON(1, 1, 11)->SUC(10, 11)
SUC(10, 11)
```

### <11, 100>
```
CON(1, 1, 11)
CON(10, 0, 100)
CON(1, 1, 11)->CON(10, 0, 100)->SUC(11, 100)
SUC(11, 100)
```

手続き中の SUC(1, 10) を SUC('', 1) に置き換えたときのそれぞれのトレースを示す.

### <0, 1>
```
CON('', 0, 0)
CON('', 1, 1)
CON('', 0, 0)->CON('', 1, 1)->SUC(0, 1)
SUC(0, 1)
```

### <1, 10>
```
SUC('', 1)
CON('', 1, 1)
CON(1, 0, 10)
SUC('', 1)->CON('', 1, 1)->CON(1, 0, 10)->SUC(1, 10)
SUC(1, 10)
```

### <10, 11>, <11, 100>
上と同様.

## 問題1.4.4.
### 11
```
SEQ(1, 1)
CON(1, 1, 11)
SEQ(1, 1)->CON(1, 1, 11)->SEQ(1, 11)
SEQ(1, 11)
CON(1, 11, 111)
SEQ(1, 11)->CON(1, 11, 111)->SEQ(11, 111)
SEQ(11, 111)
SEQ(11, 111)->FIB(11)
FIB(11)
```

### 111
```
CON(11, 111, 11111)
SEQ(11, 111)->CON(11, 111, 11111)->SEQ(111, 11111)
SEQ(111, 11111)
SEQ(111, 11111)->FIB(111)
FIB(111)
```

### 11111
```
CON(111, 11111, 11111111)
SEQ(111, 11111)->CON(111, 11111, 11111111)->SEQ(11111, 11111111)
SEQ(11111, 11111111)
SEQ(11111, 11111111)->FIB(11111)
FIB(11111)
```

## 問題1.4.5.
```
AB(1):
    AB('');
    AB(x)->CON(x, a, y)->AB(y);
    AB(x)->CON(x, b, y)->AB(y).
```

## 問題1.4.6.
```
S(1):
    SEQ(1);
    SEQ(x)->CON(x, 0, y)->SEQ(y);
    SEQ(x)->CON(x, 1, y)->S(y).
```

## 問題1.5.1.
### (a) <10, 1, 11>
```
ADD(1, '', 1)
CON(1, 0, 10)
CON('', 1, 1)
CON(1, 1, 11)
ADD(1, '', 1)->CON(1, 0, 10)->CON('', 1, 1)->CON(1, 1, 11)->ADD(10, 1, 11)
ADD(10, 1, 11)
```

### (b) <100, 10, 110>
```
CON(10, 0, 100)
CON(1, 0, 10)
CON(11, 0, 110)
ADD(10, 1, 11)->CON(10, 0, 100)->CON(1, 0, 10)->CON(11, 0, 110)->ADD(100, 10, 110)
ADD(100, 10, 110)
```

### (c) <11, 1, 100>
```
SUC(1, 10)
ADD(1, '', 1)
CON(1, 1, 11)
CON('', 1, 1)
CON(10, 0, 100)
ADD(1, '', 1)->CON(1, 1, 11)->CON('', 1, 1)->SUC(1, 10)->ADD(11, 1, 100)
ADD(11, 1, 100)
```

## 問題1.5.2.
```
MUL(3):
    MUL(x, 0, 0);
    MUL(0, x, 0);
    MUL(x, 1, x);
    MUL(1, x, x);
    MUL(x, y, z)->CON(x, 0, w)->CON(z, 0, v)->MUL(w, y, v);
    MUL(x, y, z)->CON(y, 0, w)->CON(z, 0, v)->MUL(x, w, v);
    MUL(x, y, z)->CON(x, 0, w)->MUL(w, y, v)->ADD(v, y, u)
    ->CON(x, 1, t)->MUL(t, y, u);
    MUL(x, y, z)->CON(y, 0, w)->MUL(x, w, v)->ADD(x, v, u)
    ->CON(y, 1, t)->MUL(x, t, u).
```

## 問題1.5.3.
### (a)
これでいいのか.
```
LETTER(1):
    LETTER(a_i). // 1 <= i <= n
```

### (b)
```
SAMELENGTH(2):
    SAMELENGTH('', '');
    LETTER(x)->LETTER(y)->SAMELENGTH(x, y);
    SAMELENGTH(x, y)->LETTER(z)->LETTER(w)
    ->CON(x, z, v)->CON(y, w, u)->LETTER(v, u).
```

### (c)
```
SHORTER(2):
    SHORTER('', x);
    SHORTER(x, y)->LETTER(z)->CON(y, z, w)->SHORTER(x, w);
    SHORTER(x, y)->LETTER(z)->LETTER(w)->CON(x, z, v)->CON(y, w, u)
    ->SHORTER(v, u).
```

### (d)
```
DIFFERENT_LENGTH(2):
    SHORTER(x, y)->DIFFERENT_LENGTH(x, y);
    DIFFERENT_LENGTH(x, y)->DIFFERENT_LENGTH(y, x).
```

### (e)
```
EQUAL(2):
    EQUAL(x, x);
```

### (f)
わからない.
```
DIFFERENT_LETTER(2):
    DIFFERENT_LETTER(a_i, a_j); // i < j
    DIFFERENT_LETTER(x, y)->DIFFERENT_LETTER(y, x).
```

### (g)
```
NOT_EQUAL(2):
    SAMELENGTH(x, y)->DIFFERENT_LETTER(z, w)->CON(x, z, v)->CON(y, w, u)
    ->NOT_EQUAL(v, u);
    SHORTER(x, y)->NOT_EQUAL(x, y);
    NOT_EQUAL(x, y)->NOT_EQUAL(y, x).
```

### (h)
```
SUBWORD(2):
    SUBWORD(x, x);
    SUBWORD('', x);
    EQUAL(x, y)->LETTER(z)->CON(y, z, w)->SUBWORD(x, w);
    EQUAL(x, y)->LETTER(z)->CON(z, y, w)->SUBWORD(x, w).
```

## 問題1.5.4.
y = f(x)をf(x, y)で表わす.
以下の手続きにより, hのグラフの計算手続きが存在することが示される.
```
h(2):
    g(x, y)->f(y, z)->h(x, z).
```

また, A, BをL^{\*}の部分集合とし,

f: A -> L^{\*},

g: B -> L^{\*}

であるとする.
h(x) = f(g(x))を実現するためには, g(x)がAに属していることを確かめればよい.
具体的には, 集合Aを出力とする手続き A(1) を用意し,
```
h(2):
    g(x, y)->A(y)->f(y, z)->h(x, z).
```
とすればよい.

## 問題1.6.1.
解釈 I が作業領域 W における NAME のモデルならば, NAME 中のすべての文が真となるから,
NAME のトレースの各文はモデル I の下で真となる.
したがって, <t\_1, ..., t\_n> が W 上での NAME の出力ならば, <t\_1, ..., t\_n> は関係
NAME^{I} に属す.

## 問題1.6.2.
解釈 I を次のように定義すると, I は基本作業領域において手続き ODD のモデルとなる.
CON に連接関係, EVEN に偶数長の語の集合, ODD に奇数長の語の集合を割り当て,
その他の識別子にはすべて空集合を割り当てる.

## 問題1.6.3.
手続きに書いてあることをそのまま日本語にするしかないがどうすれば……

解釈 I を次のように定義すると, I は基本作業領域において手続き FIB のモデルとなる.
* CON に連接関係を割り当てる.
* SEQ には <1, 1> を含む, <x, y> \in SEQ に対して, <y, xy> を含む集合を割り当てる.
* FIB には <x, y> \in SEQ の2項を含む集合を割り当てる.
* その他の識別子にはすべて空集合を割り当てる.

## 問題1.7.1.
つまらない例

* I\_0: { a, ab, abb, ... }
* I\_1: { a, ab, abb, ..., b }
* I\_2: { a, ab, abb, ..., b, ba }
* I\_3: { a, ab, abb, ..., b, bba }
* I\_4: { a, ab, abb, ..., b, ba, bba }

## 問題1.7.2.
EVEN のモデルとなる解釈 I\_0, I\_1, ..., I\_4 を以下に示す.
* I\_0: 偶数語長の語の集合
* I\_1: 奇数語長の語の集合を割り当てる ODD の補集合
* I\_2: 語長が2の倍数または3の倍数の語の集合
* I\_3: 語長が2の倍数または5の倍数の語の集合
* I\_4: すべての語の集合
I\_0 = I\_1であり, i = 1, 2, 3, 4に対して, I\_0 <= I\_iである.
またi = 0, 1, 2, 3に対して, I\_i <= I\_4である.
I\_0 = I\_1 <= I\_2かつI\_0 = I\_1 <= I\_3であるが,
I\_2 <= I\_3でもI\_3 <= I\_2ではない.
これらの順序関係を表わす図式を以下に示す.
```
       I_4
      /   \
    I_2   I_3
      \   /
    I_0 = I_1
```

## 問題1.7.3.
日本語でおｋ.

I が手続き NAME の自明なモデルならば, NAME 中のすべての文が I の下で
真となるから, は が W 上で実際に NAME のモデルとなる.

## 問題1.7.4.
この族の共通解釈を I とする.
### (a)
変数を含む場合も示さないといけない？

任意の i に対して, I <= I\_i であるから, IDENTIFIER(t\_1, ..., t\_n) が I の下で
真であるとき, I\_i の下でも真である.
I に <s\_1, ..., s\_n> \notin I を加えた 解釈を I\_0 とおくと, ある i に対して,
IDENTIFIER(s\_1, ..., s\_n) が I\_i の下で真ではない.

### (b)
各 i で解釈 I\_i は W 上の解釈であるから, その族の共通解釈 I も W 上の
解釈である.

## 問題1.7.5.
### (a)
日本語でおｋ. 理解が合ってるかわからない.

各識別子 IDENTIFIER に対して, <t\_1, ..., t\_n> が NAME の出力であるとき,
トレースの最後の文が IDENTIFIER(t\_1, ..., t\_n) となる.
この IDENTIFIER が関係 IDENTIFIER^I に属すので, I は W における NAME
のモデルである.

### (b)
<t\_1, ..., t\_n> が W 上の NAME の出力に属さないとき, (a) の解釈 I の下では
<t\_1, ..., t\_n> は関係 NAME^I に属さない.

### (c)
(a) で構成したモデル I が最小モデルでないと仮定すると, ある手続き P において,
関係 IDEINTIFIER^I に属し, P の出力でない <t\_1, ..., t\_n> が存在する.
しかし, それは I の定義に矛盾する.
