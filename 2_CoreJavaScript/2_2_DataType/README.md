# データ型

## 基本データ型

* 数値
* 文字列
* 論理値

## オブジェクト型

* 基本データ型のラッパーオブジェクト
  * Number
  * String
  * Boolean
* 配列：データにindexを付けて順序付けてしたオブジェクトを配列という。

## リテラル

JavaScriptの中で直接記述することができる値のことをリテラルという。
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


### 5. 配列リテラル


### 6. オブジェクトリテラル


### 7. 関数リテラル



## 特別な値

JavaScriptでは特別なデータ値がある。

* null
* undefine

## データ変換

*
