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
* do...while文
* while文
* label文
* break文
* continue文
* return文
* for...in文
* for...of文


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

### do...while文

### while文

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

### for...of文


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

```
// try/catch/finally文

// catch,finallyはそれぞれ省略できるが、両方共省略することはできない。

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
* DOMException
* DOMERROR

#### ECMAScript例外
#### DOMException
#### DOMERROR

## その他

* function文
* with文

## function文

```
// function文

function getToday() {
  console.debug(new Date())
}

getToday();

// functionは厳密には文ではない。動的な振る舞いをするものが文であり、functionは静的な構造である。
// JavaScriptのコードが解析されコンパイルされると、functionは定義されるだけで実行はされない。

console.debug(addPlus1(1));

function addPlus1(calcVal) {
  return 1 + calcVal;
}

```

## with文

```
// with文

// 変数名の解決に使用する一連のオブジェクトのリストがスコープチェーン。
// このスコープチェーンを一時的に変更するときにwith文を使う。

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
