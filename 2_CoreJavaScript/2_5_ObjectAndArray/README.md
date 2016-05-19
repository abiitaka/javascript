# オブジェクトと配列

### オブジェクト

#### オブジェクトの生成とアクセス

JavaScriptにおけるオブジェクトの概念は、現実世界に実在する「もの」との対比で解釈される。

オブジェクトは、プロパティと型をもつ独立した存在である。

```
// オブジェクト生成
var car1 = new Object();
car1.make = "toyota";
car1.model = "エスクァイア";
console.debug(car1); // Object { make: "toyota", model: "エスクァイア" }

// オブジェクト初期化子を使ってオブジェクト生成
var car2 = {make : "toyota", model : "エスクァイア"};
console.debug(car2); // Object { make: "toyota", model: "エスクァイア" }

```

```
// コンストラクタの利用
var car3 = new Car("toyota", "ベルファイア");
console.debug(car3); // Object { make: "toyota", model: "ベルファイア" }

var car4 = new Car("NISSAN", "キューブ");
console.debug(car4); // Object { make: "NISSAN", model: "キューブ" }

function Car(make, model) {
  this.make = make;
  this.model = model;
}
```

```
// プロパティへのアクセス

var car2 = {make : "toyota", model : "エスクァイア"};

car2.make = "ISUZU";
console.debug(car2.make); // ISUZU

car2["make"] = "GM"; // 連想配列でプロパティにアクセス
console.debug(car2.make); // GM

var property = "make";
car2[property] = "NISSAN"; // 変数を使ってプロパティにアクセス
console.debug(car2.make); // NISSAN
```
```
// オブジェクトの入れ子

var p1 = {x:1, y:1};
console.debug(p1);

var p2 = {x:2, y:2};
var line =  {p1, p2};
console.debug(line);

p1.x = 3;
console.debug(p1);

line.p1.x = 5;
console.debug("line.p1.x:" + line.p1);
```

```
// プロパティの存在確認（全部）

for(var obj in line) {
  console.debug(obj + ":" + line[obj]);
}

// プロパティの存在確認（個別）

if("x" in p1) {
  console.debug("p1.x:" + p1.x);
}

if(p1.x !== undefined) {  // p1.x存在していて、undefinedだったらtrueになることに注意
  console.debug("p1.x:" + p1.x);
}

if(p1.x) {  // p1.xがnull、undefinedのでもない場合
  console.debug("p1.x:" + p1.x);
}
```

#### オブジェクトのメソッド定義

```
// メソッド定義

var car5 = new Car("NISSAN", "キューブ");
car5.toCar(); // Object { make: "NISSAN", model: "キューブ" }

function Car(make, model) {
  this.make = make;
  this.model = model;
  this.toCar = toCar; // ここがポイント。carオブジェクトにtoCarメソッドを定義する
}

function toCar() {
  // thisを使って、オブジェクトのプロパティを表示する。
  console.log("make:" + this.make + ", model:" + this.model);
}
```

#### オブジェクトのGetter、Setter

```
// Getter、Setter

// オブジェクト初期化子による定義
var position = {
  x:1,
  y:2,
  get xy() {
    return [this.x, this.y];
  },
  set xx(p) {
    this.x = p;
  },
  set yy(p) {
    this.y = p;
  }
};

console.debug(position.xy); // Array [ 1, 2 ]
position.xx = 10;
position.yy = 20;
console.debug(position.xy); // Array [ 10, 20 ]
```

```
// 生成済みのオブジェクトに追加する

var p = {x: 1, y:2};

Object.defineProperties(p, {
  "xy" : { get: function() {
    return [this.x, this.y];
  }},
  "xx" : { set: function(x) {
    this.x = x;
  }},
  "yy" : { set: function(y) {
    this.y = y;
  }}
});

console.debug(p.xy); // Array [ 1, 2 ]
p.xx = 10;
p.yy = 20;
console.debug(p.xy); // Array [ 10, 20 ]
```

#### Objectクラス

JavaScriptのすべてのオブジェクトは、Objectクラスを継承している。

```
// constructor

var date = new Date();
console.debug(date.constructor == Date); // true
console.debug(date.constructor == Object); // false

var p = {x:1, y:2}
console.debug(p.constructor); // function Object()

// オブジェクトの型確認
console.debug(typeof date == 'object' && date.constructor == Date); // true
console.debug(typeof date == 'object' && date instanceof Date); //　true。instanceofは、constructorプロパティを見ている。
```

```
// toString

var a = "test";
console.debug(a.toString()); // test

var aa = {x:1}  // オブジェクトの場合は、デフォルトのtoStirng()はあまり役に立たない。
console.debug(aa.toString()); // [object Object]
```

```
// toLocaleString

// オブジェクトを表すローカライズされた文字列を返す。

var b = new Date();
console.debug(b.toLocaleString()); // 2016/4/28 8:44:43
console.debug(b.toString()); // Thu Apr 28 2016 08:44:43 GMT+0900 (JST)
```

```
// valueOf

// オブジェクトを文字列以外の基本型に変換するときに利用する。

var c = new Boolean(true);
console.debug(c); // Boolean { true }
console.debug(c.valueOf()); // true
```

```
// hasOwnProperty

// オブジェクトのプロパティがあるかどうか確認する。ただし、継承したものでないプロパティに限る

var d = {x:1};
console.debug(d.hasOwnProperty("y")); // false
console.debug(d.hasOwnProperty("x")); // true
console.debug(d.hasOwnProperty("toString")); // false
```

```
// propertyIsEnumerable

// オブジェクトのプロパティがあり、継承したものでないプロパティであり、さらに、for...inで調べることができるプロパティがあるかどうか確認する。
// hasOwnPropertyと同じ内容を確認できる。

var d = {x:1};
console.debug(d.propertyIsEnumerable("y")); // false
console.debug(d.propertyIsEnumerable("x")); // true
console.debug(d.propertyIsEnumerable("toString")); // false
```

### 連想配列

任意のデータと任意の文字列を動的に関連付けられるようにするデータ構造。

```
// 連想配列

var customer = {address0:0, address1:1, address2:2, address3:3};
for (var i=0; i<4; i++) {
  console.debug(customer["address" + i]);
}

// 実行結果
// 0
// 1
// 2
// 3
```

```
// 連想配列の使い方

var portfolio = {mitubishi:250};
console.debug(portfolio); // Object { mitubishi: 250 }

portfolio["panasonic"] = 150; // 連想配列にすると文字列でプロパティを動的に作成できる。
portfolio["xaomi"] = 1000;

for(stock in portfolio) { // 動的に作成されたプロパティは for...in を利用して取得する。
  console.debug("portfolio." + stock + ":" + portfolio[stock]);
}

// 実行結果
// portfolio.mitubishi:250
// portfolio.panasonic:150
// portfolio.xaomi:1000
```

### 配列

#### 配列の生成とアクセス

```
// 初期化

var nums = [1, 2, 3, 4, 5, null]; // 配列初期化
console.debug(nums); // Array [ 1, 2, 3, 4, 5, null ]

var a = 1;
var aa = [a, a+10, a+20, a+30, undefined];
console.debug(aa); // Array [ 1, 11, 21, 31, undefined ]

var b = new Array(5, 4, 3, 2, 1); // Arrayオブジェクト
console.debug(b); // Array [ 5, 4, 3, 2, 1 ]
```

```
// read-write-add-delete, length

// read

var arrays = ["0", 1, "2", 3.0];
console.debug(arrays[0]); // "0"
console.debug(arrays[1]); // 1

// write

arrays[0] = 100;
arrays[1] = 111;
console.debug(arrays[0]); // 100
console.debug(arrays[1]); // 111

// add

arrays[4] = "test";
console.debug(arrays[4]);

// delete

console.debug(arrays);  // Array [ 100, 111, "2", 3, "test" ]
Array.shift(arrays);
console.debug(arrays);  // Array [ 111, "2", 3, "test" ]
```

```
// length

console.debug(arrays.length); // 4
arrays[50] = 0;
console.debug(arrays.length); // 51 最大のインデックスをベースに長さが決まる


// lengthを使って、配列を切り捨てる

var dogs = ["taro", "jiro", "shiro"];
console.debug(dogs.length); // 3
console.debug(dogs); Array // [ "taro", "jiro", "shiro" ]

dogs.length = 0;
console.debug(dogs.length); // 0
console.debug(dogs); Array // [ ]

```

#### 配列の繰り返し

```
var dogs = ["taro", "jiro", "shiro"];

// for
for (var i = 0; i< dogs.length; i++) {
  console.debug(dogs[i]);
}

// 実行結果
// taro
// jiro
// shiro


// forEach

dogs.forEach(function(dog) {
  console.debug(dog);
});

// 実行結果
// taro
// jiro
// shiro

// 値が張り当てられていない要素は、forEachで反復されない

dogs[5] = "jyon"
console.debug(dogs); // Array [ "taro", "jiro", "shiro", <2 個の空行>, "jyon" ]

dogs.forEach(function(dog) {
  console.debug(dog);
});

// 実行結果
// taro
// jiro
// shiro
// jyon

```
#### 配列のメソッド

```
// join

// 配列のすべての要素を文字列に連結する

var str = ["t", "e", "s", "t", "!"];
console.debug(str.join());     // t,e,s,t,!
console.debug(str.join(", ")); // t, e, s, t, !
console.debug(str.join(""));   // test!
```

```
// reverse

console.debug(str.reverse()); // Array [ "!", "t", "s", "e", "t" ]
```

```
// sort

// アルファベット順にソートする

console.debug(str.sort()); // Array [ "!", "e", "s", "t", "t" ]
console.debug(str.sort(function(a, b) { // 数値順
  return a-b ;  
}));
```

```
// concat

// 配列に要素を追加して、新しく配列を作成する

console.debug(str.concat("a")); // Array [ "t", "t", "s", "e", "!", "a" ]
console.debug(str.concat("b","c")); // Array [ "t", "t", "s", "e", "!", "b", "c" ]
console.debug(str); // Array [ "t", "t", "s", "e", "!" ]
```

```
// slice

// 指定された配列のサブ配列を返して、新しく配列を作成する

console.debug(str.slice(0, 1)); // Array [ "t" ]
console.debug(str.slice(4)); // Array [ "!" ]
console.debug(str.slice(1, -1)); // Array [ "t", "s", "e" ]
```

```
// splice

// 配列に要素を追加したり、削除したりする。ただし、新たに配列を作成しない

console.debug(str); // Array [ "t", "t", "s", "e", "!" ]
console.debug(str.splice(4, 5)); // 「!」が削除され、strは「 Array [ "t", "t", "s", "e" ]」になる
console.debug(str); // Array [ "t", "t", "s", "e" ]

console.debug(str.splice(4, 0, "!")); // 先頭から4文字目に「！」を追加する
console.debug(str); // Array [ "t", "t", "s", "e", "!" ]
```

```
// push, pop

// 先入れ後出しスタックが実現できる

var p = [];
console.debug(p); // Array [  ]
p.push(1, 2);
console.debug(p); // Array [ 1, 2 ]
p.pop();
console.debug(p); // Array [ 1 ]
p.push(3);
console.debug(p); // Array [ 1, 3 ]
```

```
// unshift, shift

var s = [];
console.debug(s); // Array [  ]
s.unshift(1);
console.debug(s); // Array [ 1 ]
s.unshift(2);
console.debug(s); // Array [ 2, 1 ]
s.shift();
console.debug(s); // Array [ 1 ]
```

### 配列のようなオブジェクト

```
// ただのオブジェクトを配列のようにする

var arrays = {};

var i = 0;
while(i < 10) {
  arrays[i] = i;
  i++;
}
arrays.length = 7;
arrays.size = 7;

for(p in arrays) {
  console.debug("arrays." + p + "=" + arrays[p]);
}

// 実行結果
// arrays.0=0
// arrays.1=1
// arrays.2=2
// arrays.3=3
// arrays.4=4
// arrays.5=5
// arrays.6=6
// arrays.7=7
// arrays.8=8
// arrays.9=9
// arrays.length=7
// arrays.size=7
```
