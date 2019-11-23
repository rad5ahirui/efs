# 2 EFS言語の族
## 2.2 EFS言語
### 問題2.2.1.
問題 2.**1**.1となっていたが, おそらく間違いだろう.
#### (a)
```
NOT_DIVIDES(2):
    NOT_ZERO(r)->REMAINDER(a, b, r)->NOT_DIVIDES(a, b).
```
#### (b)
```
EVEN(1):
    EVEN(0);
    EVEN(x)->SUM(x, 2, y)->EVEN(y).
```
#### (c)
```
NOT_EVEN(1):
    EVEN(x)->SUC(x, y)->NOT_EVEN(y).
```
#### (d)
```
POWER_OF_TWO(1):
    POWER_OF_TWO(1);
    POWER_OF_TWO(x)->PROD(x, 2, y)->POWER_OF_TWO(y).
```
#### (e)
```
NOT_POWER_OF_TWO(1):
    POWER_OF_TWO(x)->POWER_OF_TWO(y)->QUOTIENT(x, y, 2)
    ->LESS(x, z)->LESS(z, y)->NOT_POWER_OF_TWO(z).
```
#### (f)
```
POWER(2):
    NOT_ZERO(y)->POWER(1, y);
    POWER(x, y)->PROD(x, y, z)->POWER(z, y).
```
#### (g)
```
NOT_PRIME(2):
    NOT_PRIME(0);
    NOT_PRIME(1);
    NOT_ZERO(q)->LESS(b, a)->QUOTIENT_AND_REMAINDER(a, b, q, 0)
    ->NOT_PRIME(a).
```
#### (h)
```
RELPRIME(2):
    NOT_ZERO(a)->NOT_ZERO(b)->PROD(a, x, p)->PROD(b, y, q)
    ->SUM(p, q, 1)->RELPRIME(a, b).
```
#### (i)
```
BASE_TWO_LENGTH(2):
    BASE_TWO_LENGTH(0, 1);
    BASE_TWO_LENGTH(1, 1);
    NOT_ZERO(x)->BASE_TWO_LENGTH(x, y)->SUC(x, z)->POWER_OF_TWO(z)
    ->SUC(y, w)->BASE_TWO_LENGTH(z, w);
    NOT_ZERO(x)->BASE_TWO_LENGTH(x, y)->SUC(x, z)->NOT_POWER_OF_TWO(z)
    ->BASE_TWO_LENGTH(z, y).
```

## 2.3 2分木
### 問題2.3.1.
```
SUBTREE(2):
    IMSUB(x, l, r)->SUBTREE(x, x);
    IMSUB(x, l, r)->SUBTREE(x, l);
    IMSUB(x, l, r)->SUBTREE(x, r);
    SUBTREE(x, y)->SUBTREE(z, w)->SUBTREE(x, w).
```

### 問題2.3.2.
a, bを異なる原子記号とする.
```
NUM(2):
    NUM(b);
    NUM(x)->IMSUB(y, a, x)->NUM(y).
```

### 問題2.3.3.
```
SUC(2):
    NUM(x)->IMSUB(y, a, x)->SUC(x, y).
```

### 問題2.3.4.
```
LESS(2):
    SUC(x, y)->LESS(x, y);
    LESS(x, y)->SUC(y, z)->LESS(x, z).
```

### 問題2.3.5.
```
DEPTH_OF(2):
    ATOM(a)->NUM(b)->DEPTH_OF(a, b);
    DEPTH_OF(x, y)->IMSUB(z, w, v)->SUC(y, u)->DEPTH_OF(z, u).
```

### 問題2.3.6.
```
SAME_DEPTH(2):
    DEPTH_OF(x, y)->DEPTH_OF(z, y)->SAME_DEPTH(x, z).

NOT_SAME_DEPTH(2):
    LESS(x, y)->DEPTH_OF(z, x)->DEPTH_OF(w, y)->NOT_SAME_DEPTH(z, w).
    NOT_SAME_DEPTH(x, y)->NOT_SAME_DEPTH(y, x).
```

### 問題2.3.7.
```
NOT_EQUAL(2):
    NOTEQ(x, y)->NOT_EQUAL(x, y);
    ATOM(x)->ATOM(y)->NOTEQ(z, w)->IMSUB(v, x, z)->IMSUB(u, y, w)
    ->NOT_EQUAL(v, u);
    NOT_EQUAL(x, y)->NOT_EQUAL(y, x);
    NOT_EQUAL(x, y)->SUBTREE(z, x)->NOT_EQUAL(z, y).
```

### 問題2.3.8.
```
REPLACE(4):
    ATOM(x)->ATOM(y)->REPLACE(x, x, y, y);
    REPLACE(x, y, z, w)->REPLACE(u, y, z, v)
    ->IMSUB(s, x, u)->IMSUB(t, w, v)->REPLACE(s, y, z, t).
```

## 2.4 集合
### 問題2.4.1.
```
MEMBER_OF(2):
    ATOM_OF(x, y)->MEMBER_OF(x, y);
    ADDMEM(x, y, z)->MEMBER_OF(y, z).
```

### 問題2.4.2.
`ADDMEM`の定義から`x`は集合だからこれでおｋ?
```
SET(1):
    ADDMEM(x, y, z)->SET(x).
```

### 問題2.4.3.
```
SUBSET(2):
    SET(x)->SUBSET(x, x);
    SET(x)->ADDMEM(x, y, z)->SUBSET(x, z);
```

### 問題2.4.4.
```
UNION(3):
    SET(x)->UNION(x, x, x);
    UNION(x, y, z)->ADDMEM(x, u, v)->ADDMEM(y, s, t)->UNION(v, t, z);
    UNION(x, y, z)->UNION(x, z, y).
```

### 問題2.4.5.
「xが集合の集合で, xに属する**各**集合に要素yをつけ加えて得られる
集合の集合がzであるような3つ組<x, y, z>全体」←えっ?
```
ADD_TO_MEMBERS_OF(3):
    SET(x)->
```

### 問題2.4.6.
```
POWER(2):
    
```
