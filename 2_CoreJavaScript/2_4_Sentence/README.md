# 文

文は、大きく以下に分けることができます。

1. 制御文
* ループ文
* エラー文
* その他

## 1.制御文

* if文
* switch文

### if文

```
// if
var a = 1
if(a == 1) { // true
  console.debug("true");
}


// if...else

a = 2
if(a == 1) { // false
  console.debug("true");
} else {
  console.debug("false");
}
```

### swtich文

```
// switch

var katachi = "maru";

switch(katachi) { // maru!
  case "maru":
    console.debug("maru!");
    break;
  case "sankaku":
    console.debug("sankaku!");
    break;
  default:
    console.degbu("nothing");
}

// switch 応用

function convert(x) {
  switch(typeof x) {
    case "number":
      return x.toString(16); // 16進数に変換
    case "string":
      return "'" + x + "'"; // シングルクォートで囲む
    default:
      return x;
  }
}
console.debug(convert(10));     // a
console.debug(convert("test")); // 'test'

```

## 2.ループ文

* for文
* while文
* do...while文
* label文
* break文
* continue文
* return文
* for...in文

### for文

```
// for文

for(var count=0,i=1,j=1; i<=10; i++,j++) {
  count = i + j;
  console.debug(count);
}

// for文(カンマで複数利用)

for(var count=0,i=1,j=1; i<=10; i++,j++) {
  count = i + j;
  console.debug(count);
}

```

### while文

```
// while

var i = 0;
while(i < 0) {
  console.debug("count:" + i); // 条件に一致しない場合は、表示されない
  i++;
}

var j = 0;
while(j < 10) {
  console.debug("count:" + j);
  j++;
}
```

### do...while文

```
// do...while

var i = 0;
do {
  console.debug("count:" + i); // 必ず1回目は実行される
  i++;
} while(i < 0);

var j = 0;
do {
  console.debug("count:" + j);
  j++;
} while(j < 10);

```

### label文

```
// break + ラベル

outer:
  for(var i=0; i<5; i++) {
    console.debug("i=" + i);

    inner:
    for(var j=0; j<5; j++) {
      console.debug(" j=" + j);
      if(i == 1) {
        break inner;
      }
      if(i > 2) {
        break outer;
      }
    }
  }

```

### break文

```
// break

for(var i=0; i<10; i++) {
  if(i == 5) {
    break;
  }
  console.debug(i);
}

```

### continue文

```
// cotinue

for(var i=0; i<10; i++) {
  if(i > 3) {
    continue;
  }
  console.debug(i);
}

```

### return文

```
// return文

function isNull(obj) {
  if(obj == null) {
    return;
  }
  console.debug("obj not null.")
}

isNull(null);
isNull(new Date());

```

### for...in文

for...in文は、あるオブジェクトに属するプロパティの全てを調べるときに利用する。

```
// for in

var a = {x:1, y:2, z:3};
for(var b in a) {
  console.debug("a." + b + " = " + a[b] + "  (" + b + ")" );
}

```

## 3.エラー文

### エラー文
* throw文
* try...catch文
* 例外


### throw文

```
// throw文

factorial(-1); // Exception: Error: x must be negative.
//factorial(10); // 55

function factorial(x) {
  if(x < 0) {
    throw new Error("x must be negative.");
  }

  for(var i=1; x>1; i+=x,x--) {
    console.debug(x);
  }
  console.debug(x);  
  console.debug(i);
  return i;
}

```

### try...catch文

catch,finallyはそれぞれ省略できるが、両方共省略することはできない。

```
// try/catch/finally文

try {
  var n = prompt("Please enter a positive integer.", "");
  factorial(n);
} catch(ex) {
  console.error(ex); // -1を入力するとエラー
}

function factorial(x) {
  if(x < 0) {
    throw new Error("x must be negative.");
  }

  for(var i=1; x>1; i*=x,x--) {
    console.debug(x);
  }
  console.debug(x);  
  console.debug(i);
  return i;
}
```

```
// try-finally

var a = ["a", 1, 2, 3, 4, 5];
var i = 0, total = 0;

while(i < a.length) {
  try {
    if((typeof a[i] != "number") || isNaN(a[i]))
      continue;
    total += a[i];
  } finally {
    console.debug(i++);  // continueが使われてもカウントアップする。
  }
}

```

### 例外

* ECMAScript例外
* DOMException例外
* DOMERROR

##### ECMAScript例外

JavaScriptでは、Erorrオブジェクト以外に7つの中核的なオブジェクトがある。

* Error
* EvalError
* InternalError
* RangeError
* ReferenceError
* SyntaxError
* TypeError
* URIError

##### DOMException例外

DOMException例外は、メソッドやプロパティを使用した時の例外。

**ブラウザによって実装されていないものがあるため注意すること**

##### DOMError

DOMErrorとエラーの型

|型     |説明|
|:-----:|:------:|
|IndexError|許可された範囲内でない|
|HierarchyRequestError|ノードツリー階層不正|
|WrongDocumentError|誤ったオブジェクトがある|
|InvalidCharacterError|不正な文字|
|NoModificationAllowedError	|オブジェクト修正不可|
|NotFoundError|オブジェクト未存在|
|NotSupportedError|命令のアンサポート|
|InvalidStateError|オブジェクト不正|
|SyntaxError|文字列ミスマッチ|
|InvalidModificationError|オブジェクト修正不可|
|NamespaceError|XML名前空間不許可|
|InvalidAccessError|引数アンサポート|
|TypeMismatchError|型ミスマッチ|
|SecurityError|非安全|
|NetworkError|ネットワーク失敗|
|AbortError|命令失敗|
|URLMismatchError|URLミスマッチ|
|QuotaExceededError|容量超え|
|TimeoutError|タイムアウト|
|InvalidNodeTypeError|ノード不正|
|DataCloneError|クローン不可|

```
throw new DOMError(NetworkError);  // Exception: ReferenceError: NetworkError is not defined

```

## 4.その他

* function文
* with文

### function文

```
// function文

function getToday() {
  console.debug(new Date())
}

getToday();

```

functionは厳密には文ではない。動的な振る舞いをするものが文であり、functionは静的な構造である。
JavaScriptのコードが解析されコンパイルされると、functionは定義されるだけで実行はされない。

```
console.debug(addPlus1(1));

function addPlus1(calcVal) {
  return 1 + calcVal;
}

```

### with文

変数名の解決に使用する一連のオブジェクトのリストがスコープチェーン。
このスコープチェーンを一時的に変更するときにwith文を使う。

**パフォーマンスや可読性を考慮すると、推奨されない。**

```
// with文

var a, x, y;
var r = 10;

with(Math) {
  a = PI * r * r;
  x = r * cos(PI);
  y = r * sin(PI / 2);
}
console.debug(a);
console.debug(x);
console.debug(y);

```
