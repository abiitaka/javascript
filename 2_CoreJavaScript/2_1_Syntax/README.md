# JavaScript文法

## 文字コード

JavaScriptの文字コードは、Unicodeを使用している。

**ECMAScript標準よりも前のバージョンでは、Unicodeをサポートしていない。**

## 基本

JavaScriptは、大文字と小文字を区別する。
また、セミコロン(;)で文と文の区切りをつける。
空白や改行は、区切りではないため、無視される文字列なので注意すること。

```同じ意味
a=0;
b=0;

a=0;b=0;

```

## コメント

コメントのネストは出来ない。

```コメント
// これは１行コメント

/* この書き方でも１行コメント */

/* 複数行コメントできる
 *
 *
 */

```

## 宣言

1. 変数
* 変数の評価
* 変数のスコープ
* 変数の巻き上げ

### 1. 変数

* var
* let (ES6)
* const (ES6)

JavaScriptは、変数に型を意識しない。
特徴的なものとして、自動型変換がある。それがあるので、型を石関せず簡潔にプログラミングできる。

#### var

JavaScriptは型に厳密ではないため、varを利用すれば数値、文字列、真偽値等、どの型であってもvarで宣言できる。

関数内で宣言された場合は、関数内のスコープになる。
関数外で宣言された場合は、グローバルスコープになる。また、varを宣言していない変数も、グローバル変数となる。

#### let (ES6)

let変数は、ブロックスコープ内の局所的な変数として宣言できる。

**ただし、ブラウザのによっては、未サポートのものもあるので注意が必要。**

```
var x = true;

if(x) {
  let a = "test1";
  var b = "test2";
  c = "test3";

  console.debug(a); // test1
  console.debug(b); // test2
  console.debug(c); // test3
  console.debug(x); // true
}

// console.debug(a); // Exception: ReferenceError: a is not defined
console.debug(b); // test2
console.debug(c); // test3
console.debug(x); // true

```

#### const (ES6)

読み取り専用の定数として宣言できる。

**ただし、ブラウザのによっては、未サポートのものが多いので注意が必要。**

### 2. 変数の評価

```
//var a;
var b;
var c = null;
var d = true;

//console.debug(a); // Exception: ReferenceError: a is not defined
console.debug(b); // undefined
console.debug(c); // null
console.debug(d); // true

```

```
var x;
if(x === undefined) { // true
  console.debug(true);
} else {
  console.debug(false);
}

var y;
console.debug(y + 1); // NaN

var z = null;
console.debug(z + 1) // 0 + 1 = 1

```

### 3. 変数のスコープ

* ローカルスコープ
* グローバルスコープ

ローカルスコープは、局所的な箇所でしか利用できないスコープ。
グローバルスコープは、どこからでも利用できるスコープ。

EM5までは、ブロックレベルのスコープはない。最小単位は、関数全体になる。
EM6から一部のブラウザで利用できるlet変数がある。

```
// ローカル変数の確認
var s = "global";

function check() {
  var s = "local";
  console.debug(s); // local
}

check();

```

```
// グローバル変数の確認
s = "global";

function check() {
  s = "local";
  console.debug(s); // local

  m = "mylocal";
  console.debug(m); // mylocal
}

check();
console.debug(s); // local
console.debug(m); // mylocal

// グローバル変数でもvarをつける
var s = "global";

function check() {
  var s = "local";
  console.debug(s); // local

  var m = "mylocal";
  console.debug(m); // mylocal
}

check();
console.debug(s); // global
console.debug(m); // mylocal

```

```
// ブロックレベルのスコープはない
var scope = "global";

function f() {
  console.debug(scope); // globalではなく、undefinedが表示される。これは関数内のscope変数がまだ宣言されてないからである。
  var scope = "local";
  console.debug(scope); // local
}

f();

```

### 4. 変数の巻き上げ

例外を発生させることなく、後に宣言した変数を参照することができる。

　**基本的に利用しないほうがいい。**

```
var x = "test";

(function(){
  var x;
  console.debug(x); // undefined
  x = "foo";
  console.debug(x); // foo
})();

```

## リテラル

リテラル＝データの値

※詳細は、データ型の章で説明する。

```リテラルの種類
100                //数値
3.14               //数値（小数点）
"おはよう"          //文字列
'こんにちは'        //文字列
true              //論理値
false             //論理値
null              //オブジェクトがない
{id=1, name="a"}  //オブジェクト
[1,2,3,4,5]       //配列

```

## その他

### 予約後

JavaScript、ECMAScriptの予約後は使用しないようにする。

### ガーベージコレクション

JavaScriptにも、Javaと同じようにガーベージコレクション機能がある。

**メモリ管理は、JavaScriptインタプリタが自動で開放する。**
