# 関数

### 関数の定義

関数は、以下の内容で定義される。

* functionキーワードを使う。
* その後ろに名前をつける。
* その後ろに引数を丸括弧「()」で囲む。引数が複数あれば「,(カンマ)」で区切る。
* 関数本体を定義するため、中括弧「{}」で囲む

```
function calc(a, b) {
  return a * b;
}

console.debug(calc(2, 3)); // 6
```

### 関数リテラル

関数リテラルは、無名関数を定義する式。

**function文は、構文上は文であり、関数名が必要。関数リテラルは、構文上は式であり、関数名が不要になる。**  
ただし、関数リテラルに関数名を指定するこもできる。

関数リテラルは、1回しか使わない関数や名前をつける必要のない関数に適している。

```
//function文

function calc_f(x) {return x * x};
console.debug(calc_f(5)); // 25


// 関数リテラル

var calc_r = function(x) {return x * x;}
console.debug(calc_r(5)); // 25


// 関数リテラルに名前をつける

var calc_rn  = function calc(x) {
  if(x <= 1) {
    return 1
  } else {
    return x + calc(x-1);
  }

}
console.debug(calc_rn(10)); // 55
```

### 関数の命名規則

* 動詞そのものや動詞から始まる語句
* 先頭は小文字から始める
* 単語の区切りには、以下の区切り方がある
  - get_data のように、アンダースコアで区切る
  - getData のように、単語の始まりは大文字で区切る
* 内部でしか使用しないprivateな関数には、アンダースコアからはじまる名前をつける

### 関数の引数

JavaScriptは型を意識しないので、関数定義時に引数の型をつける必要はない。

```
// 省略可能な引数

// 引数を省略することができる。省略した場合、未定義が設定される。

function toArray(a, b) {
  var result = null;
  if(!a) {
    result = [];
  } else {
    result = [a, b]
  }
  return result;
}

console.debug(toArray()); // Array [ ]
console.debug(toArray(null, 2)); // Array [ ]
console.debug(toArray(1, 2)); // Array [ 1, 2 ]
console.debug(toArray(1)); Array [ 1, undefined ]
```

#### Argumentsオブジェクト

関数の引数を管理しているオブジェクトがArgumentsオブジェクトである。  
argumentsプロパティでアクセスする。

```
// argumentsプロパティで引数を確認する

function f(a, b) {
  console.debug(arguments.length);
  console.debug(arguments[0]);
  console.debug(arguments[1]);
}

f(1,2);

// 実行結果　
// 2
// 1
// 2
```

任意の個数の引数を受け取ることができる関数を **varargs関数**（バーアーグス）=可変長引数関数 と呼ぶ。

```
// argumentsの使い方

function max() {
  var m = Number.NEGATIVE_INFINITY // -Infinity

  for(var i=0; i<arguments.length; i++) {
    if(m < arguments[i]) {
      m = arguments[i];
    }
  }
  console.debug(m);
}

max(); //-Infinity
max(1); // 1
max(100, 1); // 100
```

#### 引数にオブジェクトを渡す

オブジェクトリテラルを使えば、名前／値のペアを関数に渡すことができる。

```
function getXAndY(p) {
  return [p.x, p.y];
}

var p = {x:1, y:1, z:1};
console.debug(getXAndY(p)); // Array [ 1, 1 ]
```

#### 引数の型

JavaScriptは型付きが弱い言語である。  
そのため、関数定義時には引数の型を宣言することができない。
保守性やメンテナンス性を考慮すると、引数の型がどの型なのかわかるようにコメントで記載するとよい。

```
// 引数にコメントを付ける場合

function arraycopy(/* Array */from , /* Array */to, /* int 省略可 */from_start, /* int 省略可 */from_end, /* int 省略可 */length) {
  console.debug(from instanceof Array); // true
  console.debug(to instanceof Array); // true
  console.debug(typeof from_start); // number
  console.debug(typeof from_end); // number
  console.debug(typeof length); // number
  return;
}

var from = [1, 2, 3];
var to   = [];
arraycopy(from, to, 0, 10, 0);
```

```
// 引数の型を厳密にチェックする場合

function flex_is_sum(a) {
  var total = 0;

  for(var i = 0; i < arguments.length; i++) {
    var element = arguments[i];
    console.debug(i + ":" + element);
    if(!element) continue;

    var n;
    switch(typeof element) {
      case "number": // 数値
        n = element;
        break;
      case "function": // 関数
        n = element();
        break;
      case "string": // 文字列の場合、数値に変換
        n = parseFloat(element);
        break;
      case "boolean": // 論理値
        if(element == true) n = 1;
        if(element == false) n = 1;
        break;
      case "Object": // オブジェクト
        if(element instanceof Array) {
          n = flex_is_sum(element);
        } else {
          n = element.valueOf();
        }
        n = element;
        break;
    }

    console.debug(i + ":" + n);
    if(typeof n == "number" && !isNaN(n)) {
      total += n;
    } else {
      throw new Error("sum(): can't convert ["+ element + "] to number.");
    }
  }
  return total;
}


console.debug(flex_is_sum(1,"1",true)); // 3
```


### データとしての関数

関数はデータとして扱える。

```
function calc(x) {
  if(x == 0) return 1;
  return x * calc(x-1);
}

var a = calc(3)
console.debug(a); // 6

var b = calc; // 関数を代入
console.debug(b(4)); // 24

var c = {props: calc}; // オブジェクトのプロパティに代入
console.debug(c.props(5)); // 120
```

```
// 関数をデータとして使用する方法

function add(x, y) { return x + y; }
function subtrat(x, y) { return x - y; }
function multiply(x, y) { return x * y; }
function divide(x, y) { return x / y; }

function o(func, x, y) {
  return func(x, y);
}

// (2+3) + (4*5)
var l = o(add, 2,3);
var r = o(multiply, 4,5);
console.debug(o(add, l, r)); // 25
```

### メソッドとしての関数

JavaScriptのメソッド・・・オブジェクトのプロパティに格納されているJavaScriptで、このオブジェクトを介して呼び出される関数のこと。

```
function add(a, b) {
  return a + b;
}

var o = {m: null };

o.m = add; // addメソッド
console.debug(o.m(1, 2)); // 3
```

**メソッドには、重要なポイントが一つある。**  
**メソッドを呼び出すときに使用したオブジェクトが、メソッド本体の中でthisキーワードの値になる。**

```
var calc = {
  x: 0,
  y: 0,
  add: function() {
    return this.x + this.y;
  }
};

calc.x = 1;
calc.y = 2;
console.debug(calc.add()); // 3
```

#### thisキーワード

メソッドとして使用する関数には、通常の引数とは別に、呼び出すときに指定したオブジェクト自身が渡される。

注意点
* 関数がメソッドではなく関数として呼び出された場合、thisキーワードはグローバルオブジェクトを参照する。
* メソッドとして呼び出された関数の中に入れ子にされた別の関数が関数として呼び出された場合も、グローバルオブジェクトを参照する。

### 関数のプロパティとメソッド

#### length

* arguments.length
* 関数のlength＝引数.callee.length

argumentsのlengthは、関数に渡された引数の個数。
関数のlengthは、関数に渡されるはずの引数の個数。つまり、引数リストに宣言された引数の個数

```
function check(args) {
  var actual = args.length;
  var expected = args.callee.length;
  console.debug("args.length:" + args.length);
  console.debug("args.callee.length:" + args.callee.length);

  if(actual != expected) {
    throw new Error("Wrong number of arguments: expected:" + expected + ";actually passed " + actual);
  }
}

var add = function(x, y, z) {
  check(arguments);
  return x + y + z;
}

// 宣言した引数と渡した引数の数が同じ場合
console.debug(add(1, 2, 3)); // 6

// 宣言した引数と渡した引数の数が異なる場合
console.debug(add(1, 2)); // Exception: Error: Wrong number of arguments: expected:3;actually passed 2
```

#### 自分専用の関数プロパティの定義

自分専用の関数プロパティを宣言すると、関数内部からしか使用させない構成にすることができる。
ただし、外部から値が変更されることを考慮しなければならない。  
以下のいずれのパターンも、外部から値を変更することができる。

```
// グルーバル変数をもつ
// グローバル変数のため、変数名が重複する可能性がある
var g_counter = 0;

function g_calc() {
  return g_counter++;
}

console.debug("g_counter:" + g_calc()); // 0
console.debug("g_counter:" + g_calc()); // 1
console.debug("g_counter:" + g_calc()); // 2
console.debug("g_counter:" + g_calc()); // 3

// Function関数内に変数をもつ
f_calc.f_counter=0;

function f_calc() {
  return f_counter++;
}

console.debug("f_counter:" + f_calc()); // 0
console.debug("f_counter:" + f_calc()); // 1
console.debug("f_counter:" + f_calc()); // 2
console.debug("f_counter:" + f_calc()); // 3
```

#### applyメソッドとcallメソッド

あるオブジェクトのメソッドであるかのうように関数を呼び出すことができる。

```
var add = function(x, y) {
  return x + y;
}

var calc = {
  minus : function(x, y) {
    return x- y;
  }
}

console.debug(add.call(calc, 10, 3)); // 13
```

以下と同じ意味。

```
calc.add = add;
console.debug(calc.add(10, 3)); // 13
delete calc.add;
```

### ユーティリティ関数

```
// 指定したパラメータのプロパティ名を配列で返却するユーティリティ

function getPropertyNames(/* オブジェクト */obj) {
  var result = [];
  for(name in obj) result.push(name);
  return result;
}

var p = {x: 1, y: 2};
console.debug(getPropertyNames(p)); //Array [ "x", "y" ]
```

```
// from から to にプロパティをコピーするユーティリティ
// to がnullの場合は、新たにオブジェクトを生成する

function copyProperties(/* オブジェクト */from, /* オブジェクト */to) {
  if(!to) to = {};
  for(var p in from) to[p] = from[p];
  return to;
}

var p = {a: 1, b: 2};
var copy_p = copyProperties(p);
console.debug(p); // Object { a: 1, b: 2 }
console.debug(copy_p); // Object { x: 1, y: 2 }

var to_p = {};
console.debug(to_p); // Object {}

copyProperties(copy_p, to_p);
console.debug(to_p); // Object { x: 1, y: 2 }
```

```
// from から to にプロパティをコピーするユーティリティ
// to に未定義の場合、fromの値をコピーする。to の値はそのまま

function copyUndefineProperties(/* Object */from, /* Object */to) {
  for(var p in from) {
    if(p in to) {
      // 処理なし
    } else {
      to[p] = from[p];
    }
  }
}

var position = {x: 0, y: 0};
var tmp = {x: 1, z: 3};

copyUndefineProperties(position, tmp);
console.debug(tmp); // Object { x: 1, z: 3, y: 0 }
```

```
// 配列 a の各要素に対して、指定した第2引数の条件に一致する要素のみを抽出するユーティリティ

function fileArray(/* Array */ a, /* 論理値を返す関数 */ predicate) {
  var results = [];
  var length = a.length;
  for(var i = 0; i < length; i++) {
    var element = a[i];
    if(predicate(element)) results.push(element);
  }
  return results;
}

var gusu = function(value) {
  if(value % 2 == 0) return true;
  return false;
}

var numbers = [1,2,3,4,5,6,7,8,9,0];

console.debug(fileArray(numbers, gusu)); // Array [ 2, 4, 6, 8, 0 ]
```

```
// 関数を別のオブジェクトとして呼び出すユーティリティ

function bindMethod(/* Object */ obj, /* Function */ func) {
  return function() {return func.apply(obj, arguments)}
}

var position = {x: 1, y: 2}

var out = function() {
  console.debug("out call");
}

bindMethod(position, out)();
```

```
// 呼び出し時に指定した引数のほかに、あらかじめ指定した引数も含めて、関数funcを呼び出す関数を返す
// 　＝カリー化
function  bindArguments(/* Function */ func /*, 予め引数を指定する... */) {
  var boundArgs = arguments;
  return function() {
    var args = [];
    for(var i = 1; i < boundArgs.length; i++) args.push(boundArgs[i]);
    for(var i = 1; i < arguments.length; i++) args.push(arguments[i]);

    return func.apply(this, args);
  }
}

var calc = function(x, y) {
  return x + y;
}

var bindFunc = bindArguments(calc(1,2), 3,4);
```

### 再帰
#### calleeプロパティ

Argumentsオブジェクトのcalleeプロパティは、現在実行中の関数を参照する。  
arguments.calleeによって、無名関数は自分自身を参照することできるため、無名な再帰関数を呼び出すときに利用できる。

```
// calleeプロパティを利用しない再帰文

function fact(x) {
  var result = 0;
  if(x <= 1) {
    result = 1;
  } else {
    result = x * fact( x-1 );   
  }
  console.debug(x + " = " + result);
  return result;
}

console.debug(fact(5));

// 実行結果
// 1 = 1
// 2 = 2
// 3 = 6
// 4 = 24
// 5 = 120
// 120
```

```
// 無名関数でcalleeプロパティを利用した再帰文

var fact_ = function(x) {
  var result = 0;
  if(x <= 1) {
    result = 1;
  } else {
    result = x * arguments.callee( x-1 );
  }
  console.debug(x + " = " + result);
  return result
}

var result = fact_(5);
console.debug(result);

// 実行結果
// 1 = 1
// 2 = 2
// 3 = 6
// 4 = 24
// 5 = 120
// 120
```
