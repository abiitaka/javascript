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
ただし、関数リテラルで関数名を指定してもよい。

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
// argumentsオブジェクトで引数を確認する

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

JavaScriptのメソッド：オブジェクトのプロパティに格納されているJavaScriptで、このオブジェクトを介して呼び出される関数のこと。

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
