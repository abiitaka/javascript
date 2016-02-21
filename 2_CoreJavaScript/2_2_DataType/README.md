# データ型

## 基本データ型

* 数値
* 文字列
* 論理値
* null
* undefined

## オブジェクト型

* 基本データ型のラッパーオブジェクト
  * Number
  * String
  * Boolean
* 配列：データにindexを付けて順序付けてしたオブジェクトを配列という。

## リテラル

JavaScriptの中で直接記述することができる値のことをリテラルと呼ぶ。
リテラルには、以下がある。

1. 整数リテラル
* 浮動少数点リテラル
* 文字列リテラル
* 真偽値リテラル
* 配列リテラル
* オブジェクトリテラル
* 関数リテラル

### 1. 整数リテラル

```
var num;

num=0;
console.debug(num); // 10進数

num=10000;
console.debug(num); // 10進数

num=0xff;
console.debug(num);  // 16進数

num=0377;
console.debug(num);  // 8進数　ブラウザによって0始まりを無視するので8進数は使わない方がいい。

```
### 2. 浮動少数点リテラル

```
var num;

num = 3.14;
console.debug(num);

num = 6.02e23;
console.debug(num); // 指数

```

### 3. 文字列リテラル

```
var str;

str = 'test';
console.debug(str);  // シングルクォーテーション

str = "test";
console.debug(str);  // ダブルクォーテーション　

str = 'test"!"';
console.debug(str);  // シングルクォーテーションとダブルクォーテーション

str = "test'!'";
console.debug(str);  // シングルクォーテーションとダブルクォーテーション

str = '\'';
console.debug(str);  // シングルクォーテーションを文字列表示

str = "\"";
console.debug(str);  // ダブルクォーテーションを文字列表示

str = "te";
console.debug(str + "st");  // 文字列連結

```

### 4. 真偽値リテラル

```
var isBool;

isBool = true;
console.debug(isBool); // true

isBool = false;
console.debug(isBool); // true

```

### 5. 配列リテラル

```
var a = new Array();
a[0] = 10;         // 数値
a[1] = 'test1';    // 文字列（シングルクォーテーション）
a[2] = "test2";    // 文字列（ダブルクォーテーション）
a[3] = true;       // 論理値
a[4] = {x:0, y:1}; // オブジェクト

console.debug(a);

var b = new Array(10, 'test1', "test2", true, {x:0, y:1});
console.debug(b); //コンストラクタのパラメータに指定できる

var c = [10, 'test1', "test2", true, {x:0, y:1}];
console.debug(c); // 配列リテラル

var c = [10, , , , {x:0, y:1}];
console.debug(c); // 配列リテラル（空行）

```

### 6. オブジェクトリテラル

```
var point = {x:0, y:1};
console.debug(point); // x:0, y:1

var rect = {
  topleft:{x:0, y:0},
  topright:{x:10, y:0},
  bottomleft:{x:10, y:0},
  bottomright:{x:10, y:10}
};
console.debug(rect); // オブジェクトの入れ子

```

### 7. 関数リテラル

```

function square(x) {
  return x*x;
}
console.debug(square(2)); // 関数結果 4

var square2 = function(x){ return x*x; }
console.debug(square2(3)); // 関数リテラル 関数結果 9

```


## 特別な値

JavaScriptでは特別なデータ値がある。

* null
* undefined

### null

「値」がないことを表す特別な値。

JavaScriptでは、nullはオブジェクトが存在しないことを表す値である。また、プリミティブ型の一つである。

### undefined

undefinedは、グローバルオブジェクトのプロパティであり、ndefined変数の初期値は、プリミティブ値のundefinedである。

宣言されている値が、設定されていない変数、存在しないオブジェクトのプロパティを使うとundefinedが返却される。

**nullとは異なる値。**

### nullとundefined

```
var a
a = null;
console.debug(a); // null
console.debug(typeof null); // 型比較では、obuject。nullに本来はなるはず。ECMAScriptのバグ

var b;
console.debug(b); // 宣言だけの場合、undefined
console.debug(typeof undefied); // 型比較では、undefined

console.debug(null === undefined); //　同値演算では、false
console.debug(null == undefined); //　等値演算では、true

```

## データ変換

*
