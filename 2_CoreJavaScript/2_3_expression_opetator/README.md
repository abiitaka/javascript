# 式と演算子

## 演算子

JavaScriptの演算子

|  優先度|   結合性|  演算子| オペランドの型|
|:-----:|:------:|:------|:------------|
|15     |L       |.      |オブジェクト.識別子|
|       |L       |[]     |配列、整数|
|       |L       |()     |関数、引数|
|       |R       |new    |コンストラクタ|
|14     |R       |++     |左辺値|
|       |R       |--     |左辺値|
|       |R       |-      |数値|
|       |R       |+      |数値|
|       |R       |~      |数値|
|       |R       |!      |論理値|
|       |R       |delete |左辺値|
|       |R       |typeof |任意|
|       |R       |void   |任意|
|13     |L       |* / %  |数値|
|12     |L       |+ -    |数値|
|       |L       |+      |文字列|
|11     |L       |<<     |整数|
|       |L       |>>     |整数|
|       |L       |>>>    |整数|
|10     |L       |< <=   |数値、文字列|
|       |L       |> >=   |数値、文字列|
|       |L       |instanceof|オブジェクト、コンストラクタ|
|       |L       |in     |文字列、オブジェクト|
|9      |L       |==     |任意|
|       |L       |!=     |任意|
|       |L       |===    |任意|
|       |L       |!==    |any|
|8      |L       |&      |整数|
|7      |L       |^      |整数|
|6      |L       |&#124; |整数|
|5      |L       |&&     |論理値|
|4      |L       |&#124;&#124;|論理値|
|3      |R       |?:     |論理値 ? 任意 : 任意|
|2      |R       |=      |左辺値、任意|
|       |R       |*=     |左辺値、任意|
|       |R       |/=     |左辺値、任意|
|       |R       |%=     |左辺値、任意|
|       |R       |+=     |左辺値、任意|
|       |R       |-=     |左辺値、任意|
|       |R       |<<=    |左辺値、任意|
|       |R       |>>>=   |左辺値、任意|
|       |R       |&=     |左辺値、任意|
|       |R       |^=     |左辺値、任意|
|       |R       |&#124;=|左辺値、任意|
|1      |L       |,      |任意|

**演算子が複数ある場合は、優先度の数値が大きいほど、優先度が高くなります。**

```
// 演算子の優先順位
var a = 1;
var b = 2;
var c = 3;

x = a + b * c;
console.debug(x); // 7

y = (a + b) * c;
console.debug(y); // 9

```

## 算術演算子
1. 加算演算子
* 減算演算子
* 乗算演算子
* 除算演算子
* 剰余演算子

```
// 加算演算
console.debug(10 + 20); // 30

// 減算演算
console.debug(10 - 20); // -10

// 乗算演算
console.debug(10 * 20); // 200

// 除算演算
console.debug(10 / 20); // 0.5

// 剰余演算
console.debug(5 % 2); // 1

```

## 等値演算子

1. 等値演算子
* 同値演算子

```
// ==演算子（等値演算子）の判定ルール

function equal(a, b) {
  if(a == b) {
    console.debug("等値");
  } else {
    console.debug("不等");
  }
}

var a1 = "あ";
var b1 = "あ"
equal(a1, b1); //等値　同一の型、同じ値

var a2 = "2";
var b2 = 2;
equal(a2, b2); //等値 文字列の場合、数値型に自動変換される

var a3 = NaN;
var b3 = NaN;
equal(a3, b3); //不等（NaN同士はtrueにならない）

var a4 = true
var b4 = 1
equal(a4, b4); //等値 trueの場合、true→1に変換する

var a5 = false
var b5 = 0
equal(a5, b5); //等値 falseの場合、false→0に変換する

var a6 = [1, 2, 3];
var b6 = [1, 2, 3];
var c6 = a6;
equal(a6, b6); //不等
equal(a6[0], b6[0]); //等値 参照先は異なるが、数値として同じ値なのでtrue
equal(a6, c6); //等値 参照先が同じ場合はtrue

var a7 = null;
var b7 = null;
var c7 = undefined;
var d7 = undefined;
equal(a7, b7); //等値 両方ともnull
equal(c7, d7); //等値 両方ともundefined
equal(a7, c7); //等値 nullとundefinedの場合は、false

```

```
/ ===演算子（同値演算子）の判定ルール

function equivalence(a, b) {
  if(a === b) {
    console.debug("同値");
  } else {
    console.debug("非同値");
  }
}

var a1 = "1";
var b1 = 1
equivalence(a1, b1); //非同値 型が異なるときはtrueにならない

var a2 = 2;
var b2 = 2;
equivalence(a2, b2); //同値

var a3 = NaN;
var b3 = NaN;
equivalence(a3, b3); //非同値（NaN同士はtrueにならない）
console.debug(isNaN(a3)) //true NaNを調べる方法は、isNaNを使う

var a4 = true
var b4 = true
equivalence(a4, b4); //同値

var a5 = false
var b5 = false
equivalence(a5, b5); //同値

var a6 = [1, 2, 3];
var b6 = [1, 2, 3];
var c6 = a6;
equivalence(a6, b6); //非同値
equivalence(a6[0], b6[0]); //同値 参照先は異なるが、数値として同じ値なのでtrue
equivalence(a6, c6); //同値 参照先が同じ場合はtrue

var a7 = null;
var b7 = null;
var c7 = undefined;
var d7 = undefined;
equivalence(a7, b7); //同値 両方ともnull
equivalence(c7, d7); //同値 両方ともundefined
equivalence(a7, c7); //非同値 nullとundefinedの場合は、false

```

## 関係演算子

1. 比較演算子
* in演算子
* instanceof演算子

```
//　比較演算子

function check(a, b) {
  if(a == b) {
    console.debug("true");
  } else {
    console.debug("false");
  }
}

var e1 = 1
var e2 = 1
check(e1, e2); // true 両方と数値

var f1 = "a"
var f2 = "a"
check(f1, f2) // true 両方共文字列

var g1 = "2";
var g2 = 2;
check(g1, g2) // true 一方が文字列、一方が数値の場合、文字列は数値に変換される

var h1 = "a";
var h2 = 2;
check(h1, h2) // false 文字列は数値に変換されるが、数値でない場合はNaNに変換される

var h1 = new Date("2016","2", "10", "8", "50", "12", "111");
var h2 = "201621085012111";
check(h1, h2); // false 日付型は文字列として比較される。

var i1 = [1, 2];
var i2 = 1
check(i1, i2); // false オブジェクトが数値、文字列に変換できない場合はfalse

var j1 = NaN;
var j2 = 1;
check(j1, j2) // false NaNで比較される場合はfalse

var k1 = "\u3042";
var k2 = "あ"
check(k1, k2); // unicodeでの比較もできる

var l1 = "\u3042"; // あ
var l2 = "\u3044"; // い
console.debug(l1 + l2);

if(l1 < l2) { // true 文字列の大小判定は、unicode順
  console.debug(true);
} else {
  console.debug(false);
}

```

```
// in演算子を利用するとオブジェクトにあるロパティの存在有無が確認できる

var position = {x:1, y:2, z:3}

console.debug("x" in position); // true
console.debug("y" in position); // true
console.debug("t" in position); // false
console.debug("toString" in position); // 親オブジェクトがもつプロパティも確認できる
```

```
// instanceofは、左側のオブジェクトが右側のクラスのインスタンスかどうかが確認できる。

var s = new String("a");
console.debug(s instanceof String); // true

var n = new Number(1);
console.debug(n instanceof Number); // true

var d = new Date();
console.debug(d instanceof Date); // true
console.debug(d instanceof Object); // true
console.debug(d instanceof Number); // false

```

## 文字列演算子

```
// 文字列型に+演算子を利用すると連携する
console.debug("test" + "1"); //test1

// 文字列の比較演算子
console.debug(1 + 2);      // 3
console.debug("1" + "2");  // 12
console.debug("1" + 2);    // 12

console.debug(11 < 1);     // false
console.debug("11" < "3"); // true unicodeのアルファベット順に比較される
console.debug("11" < 3);   // 11が数値に変換されるため数値比較になる、false
console.debug("a" < 3);    // aが数値に変換されNaNになるため、false

```

## ビット演算子

**ほぼ利用しないので割愛。**


## 論理演算子

1. 論理積演算子
* 論理和演算子
* 論理否定演算子

```
// 論理演算子

var a = 1;
var b = 2;
var c = 3;
var d = 4;

function stop() {
  console.debug("stop.");
  return true;
}

// 論理積演算子 &&
console.debug(a == 1 && b ==2) // true
console.debug(a == 1 && b ==3) // false

console.debug(a == 1 && stop()) // true, stop.
console.debug(a == 2 && stop()) // false, stopは処理されない。


// 論理和演算子 ||
console.debug(c == 3 || d ==4) // true
console.debug(c == 3 || d ==5) // true

console.debug(c == 3 || stop()) // true, stop.
console.debug(c == 2 || stop()) // true, stopは処理されない。

```

```
// 論理否定演算子 !

var a = 1;
var b = 2;

console.debug(a == 1); // true
console.debug(a != 1); // false

```

## 代入演算子

```
var a = 0; // 0が代入される
console.debug(a); // 0

var b = 1, c = 2;
console.debug(b); // 1
console.debug(c); // 2

c = b = a = 3; // 複数の代入演算子
console.debug(a); // 3
console.debug(b); // 3
console.debug(c); // 3

```

## その他

1. 三項演算子
* typeof演算子
* new演算子
* delete演算子
* void演算子
* カンマ演算子

```
// 三項演算子

var i = 1;

console.debug(i == 1 ? true : false); // true
console.debug(i == 2 ? true : false); // false

```

```
// typeof 演算子

var n = 1;
console.debug(typeof n); // number

var s1 = "a";
console.debug(typeof s1); // string

var s2 = "1";
console.debug(typeof s2); // string

var b = true;
console.debug(typeof b); // boolean

var nObj = new Number(1);
console.debug(typeof nObj); // object

var sObj = new String("a");
console.debug(typeof sObj); // object

var bObj = new Boolean(true);
console.debug(typeof bObj); // object

var p = {x:1, y:2};
console.debug(typeof p); // object

var f = function() { var i = 0; };
console.debug(typeof f); // function

```
