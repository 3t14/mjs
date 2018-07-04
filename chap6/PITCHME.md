#### モダンJavaScriptプログラミング入門
# 6. ES6の基本文法2
#### 田中　充
##### 株式会社イワテシガ

Web教材: http://mj.is-good.net

---
### アロー関数 (1 / 5)
#### 基本書式
- 関数リテラルの記述がシンプルに
- **function** 記述の代わりに "**=>**"（アローを利用）

```JavaScript
// 従来のリテラル
let f1 = function(a, b) { return a * b };

// 上記をアロー関数に置き換えたもの
let f2 = (a, b) => { return a * b };
console.log(f1(2, 3)); // 6
console.log(f2(2,　3)); // 6
```

---
### アロー関数 (2 / 5)
#### thisキーワードの意味の違い
- thisの意味
 - 通常の関数内: globalオブジェクト
   - ブラウザの場合: **windowオブジェクト**
   - Node.jsの場合: **globalオブジェクト**
 - アロー関数内
   - 対象クラスのインスタンス（オブジェクト）自身

+++

```JavaScript
let MyObject = function MyObject() {
  this.i = 1;
  console.log(this); // オブジェクト自身の参照
  let f1 = function() {
    console.log(this); // コンソール上での確認用
    console.log(this.i); // undefined
  };
  f1();
  let f2 = () => {
      console.log(this); // コンソール上での確認用
      console.log(this.i); // 上記で定義したiの値1が出力される
  };
  f2();
}

let myObject = new MyObject(); // オブジェクトを生成し動作を確認
```

@[4-7](この関数内ではthis=グローバルオブジェクト);
@[9-12](この関数内ではthis=インスタンス自身);
@[2, 11](オブジェクトのプロパティiの参照が可能);

---
### 関数とnew 演算子
- 関数 → オブジェクトの一種
- **new 関数名()**
 - 新しい関数オブジェクトを生成し、その生成されたオブジェクトを返す
 - **new演算子** にかかる関数は、**コンストラクタ** の役割
  - **コンストラクタ** ＝インスタンス生成時に実行される関数

---
### アロー関数 (3 / 5)
#### 省略記法 1
```JavaScript
// return文のみの場合は{}は不要
let f1 = (a, b) => a * b;
console.log(f1(2, 3)); // 6

// 引数が一つのみの場合は()は不要
let f2 = a => a * 3;
console.log(f2(2)); // 6

// 引数がない場合は()の省略は不可
let f3 = () => 2 * 3;
console.log(f3()); // 6
```
---
### アロー関数 (4 / 5)
#### オブジェクトリテラルとデフォルト引数
```JavaScript
// オブジェクトリテラルを返す場合は()で囲む
let f4 = () => ({key: 'value'});
console.log( f4() );

// デフォルト引数も利用可能
let f5 = (a = 2, b = 3) => a * b;
console.log(f5());
```

---
### アロー関数 (5 / 5)
#### 可変長引数、分割代入、展開演算子

```JavaScript
// 可変長引数の利用
let f6 = (a, b, ...others) => {
  let c = a + b;
  for (let i of others) {
    c += i;
  }
  return c;
}
console.log(f6(1, 2, 3, 4)); // 10

// 分割代入や展開演算子の利用
let f7 = (a, b, [c, d] = [3, 4]) => a + b + c + d;
console.log(f7(...[1, 2])); // 10
```

---
### Promiseオブジェクト (1 / 8)
- 非同期処理が連なって可読性が悪くなったコールバック連鎖を改善できる、非同期処理制御オブジェクト
- コールバック関数とは
 - イベント等が発生した時に実行してほしい関数のこと
 - すぐに処理が終了しない非同期通信などで使われる
 - 処理が終了したら、あらかじめ登録したコールバック関数が呼び出される

+++

### コールバック地獄の例

```JavaScript
let i = 0;
function test(callback) {
  i++;
  console.log(i);
  callback();
}

// コールバック連鎖（コールバック地獄）何をしているのか理解が難しくなる
test(() => {
  test(() => {
    test(() => {
      test( () =>{});
    });    
  });
});
```

---
### Promiseオブジェクト (2 / 8)
#### Promiseオブジェクトを使用した例

```JavaScript
let j = 0;
function test2() {
  j++;
  console.log(j);
  return new Promise((resolve, reject) => {
    if (j > 2) reject('error');
    else resolve();
  });
}

test2()
  .then(() => test2())
  .then(() => test2())
  .catch(e => console.log(e));
```
@[11](関数test2を実行);
@[2-9](Promiseオブジェクトを返却)
@[6-7](内部のアロー式は非同期で遅延実行される);
@[12](最初のtest2の結果取得成功後の処理を登録);
@[13](２回目のtest2の結果取得成功後の処理を登録);
@[14](失敗=reject時の処理を登録);

+++

- 入れ子になっていない
- 非同期処理を行う関数（test2）の戻り値をPromiseオブジェクトにする
- 非同期処理完了後、thenメソッドが呼ばれる


---
### Promiseオブジェクト (3 / 8)
#### Promiseコンストラクタの構文

```JavaScript
new Promise((resolve,reject)=>{時間のかかる処理を記述…})
```

- **resolve**：処理成功時に呼び出す関数
- **reject**：処理失敗時に呼び出す関数
----
#### thenメソッドの構文

```JavaScript
then(onFullFilled,onRejected)
```

- **onFullFilled**：処理成功時のコールバック関数
- **onRejected**：処理失敗時のコールバック関数


---
### Promiseオブジェクト (4 / 8)
- 処理失敗時のコールバック関数は、一つにまとめることが可能

```JavaScript
// 全てに処理失敗時の関数を記述した場合、以下の順で出力
// 1, 2, 3, error3, 4, error5, 5
test2()
  .then(()=>test2(), () => console.log('error1'))
  .then(()=>test2(), () => console.log('error2'))
  .then(()=>test2(), () => console.log('error3'))
  .then(()=>test2(), () => console.log('error4'))
  .then(()=>test2(), () => console.log('error5'))
  .then(()=>test2(), () => console.log('error6'));

```
---
### Promiseオブジェクト (5 / 8)

```JavaScript
// 最後に処理失敗時の関数を記述した場合、以下の順で出力
// 1, 2, 3, error
test2()
  .then(()=>test2())
  .then(()=>test2())
  .then(()=>test2())
  .then(()=>test2())
  .then(()=>test2(), () => console.log('error'));
```

---
### Promiseオブジェクト (6 / 8)
- catch関数の利用
 - ``catch(reject)``
 - **reject**：処理失敗時のコールバック関数

 ```JavaScript
 // 最後に処理失敗時の関数を記述した場合、以下の順で出力
 // 1, 2, 3, error
 test2()
   .then(()=>test2())
   .then(()=>test2())
   .then(()=>test2())
   .catch(() => console.log('error'));
 ```

---
### Promiseオブジェクト (7 / 8)
- Promise.all関数:複数の処理を並行に実行、全て成功した場合の条件も与えられる
 - その場合、受け取る値は配列となる

 ```JavaScript
function test3(value) {
  return new Promise((resolve, reject) => {
    if (typeof value === "undefined") reject('undefined');
    else resolve(value);
  });
}
// ["value1", "value2"]を出力
Promise.all([test3('value1'), test3('value2')]) // すべてresolve
  .then(a => console.log(a), b => console.log(b));
// undefinedを出力
Promise.all([test3('value1'), test3()]) // １つrejectがあるので失敗
  .then(a => console.log(a), b => console.log(b));
```

---
### Promiseオブジェクト (8 / 8)
- Promise.race関数では、一番最初に完了した処理の結果を元に、then関数が実行される

```JavaScript
function test4(value) {
 return new Promise((resolve, reject) => {
   setTimeout( () => { // 指定したミリ秒後に処理を実行
     if (typeof value === "undefined") reject('undefined');
     else resolve(value);
   }, Math.random() * 100 ); // 乱数で実行のタイミングをずらす
 });
}
// "value1", "value2", "value3"のいずれかが出力される
Promise.race([test4('value1'), test4('value2'), test4('value3')])
 .then(a => console.log(a), b => console.log(b));
```

---
### Promiseオブジェクトの処理の流れ

![](https://mdn.mozillademos.org/files/8633/promises.png)

出典：[Promise - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Promise)

---
### Proxyオブジェクト (1 / 3)
- プロパティの設定・取得・削除・列挙など、基本的な操作をトラップし、カスタマイズするためのオブジェクト
```JavaScript
let target = {a:1, b:2};
let handler = {
  get: (target, name) => {
    // in演算子は右辺のコレクション型オブジェクトの要素に左辺が含まれるかを判定
    return name in target ? target[name] : 'not exist'; //
  }
};
let p = new Proxy(target, handler);
console.log(target.a, target.b, target.c);
console.log(p.a, p.b, p.c); // undefinedではなく'not exist'を出力
```
---
### Proxyオブジェクト  (2 / 3)
- その他の主なトラップの例

```JavaScript
let target = {a:1, b:2};
let handler = {
  set (target, key, name) { target[key] = 'set';},
  deleteProperty(target, key) { target[key] = 'delete'; },
  has(target, key) {return false;}
};
let p = new Proxy(target, handler);
p.c = 1; console.log(p.c); // set
delete p.d;
console.log(p.d); // delete; 削除されない
console.log( 'a' in p); // 含まれてるがfalseを返す
```

---
### Proxyオブジェクト  (3 / 3)
- 全てのトラップについては以下Webサイトを参照
 - [『ECMAScript® 2016 Language Specification』](http://www.ecma-international.org/ecma-262/7.0/#sec-proxy-object-internal-methods-and-internal-slots)
- 2015版ではトラップ“enumerate” が定義されていたが、2016版では削除されており、ChromeやFirefoxの最新版でも既に削除されているので注意

---
### Mapオブジェクト (1 / 2)
- キーと値でデータを管理するコレクションオブジェクト。キーに対してオブジェクトを割り当てることができる。

```JavaScript
let obj = {};
let func = () => {};
let m = new Map();
m.set('key1', 'value1'); console.log(m.get('key1'));
m.set(obj, 'value2'); console.log(m.get(obj));
m.set(func, 'value3'); console.log(m.get(func));
m.set(0.1, 'value4'); console.log(m.get(0.1));
console.log(m.size); // 要素数の取得
for (let  [k, v] of m) { // keyとvalueを分割代入で取得できる。
  console.log(k, v);
}
```

---
### Mapオブジェクト (2 / 2)
- 従来は **Object** を使用してコレクションを作成
 - **Object** と Map の違い
  - **Object** はデフォルトで特定のキーが作られる。Map には作られない。
  - ※**Object.create(null)** を使うことで回避可能
  - **Object** のキーは文字列のみ。Map は任意の値が可能
  - **Object** はサイズを取得できない。Map は簡単に取得可能
  - **Map** の各要素は、**for...of** ループで挿入順に取得可能
---
### Setオブジェクト (1 / 2)
- 一意な値を格納するオブジェクト
- 同じ値を格納しようとしても無視される
- **func** と **()=>{}** は別の値

```JavaScript
let func = () => {};
let s = new Set();
s.add(1);
s.add(1); // 無視される
s.add("value");
s.add(func);
s.add(()=>{})
console.log(s.has(1)); // true
console.log(s.has(3)); // false
console.log(s.has(func)); // true
console.log(s.has({})); // false // リテラル表記のため

for (let v of s) { // ofで個々の要素取得可能
  console.log(v);
}
```


---
### Setオブジェクト (2 / 2)
- コンストラクターに配列を渡すと、要素が展開されて、別々の値として格納される
- 同じ値は無視される

```JavaScript
let obj = {};
let func = () => {};

// 重複を除去
let s = new Set([1, 1, 'value', obj, func, {}]);
// 1, value, Object {}, () => {}, Object {}
for (let v of s) { // ofで個々の要素取得可能
  console.log(v);
}
```

---
### クラス定義 (1 / 6)
- JavaやC#などの言語と同じようにクラスを定義

```JavaScript
class Car {
  constructor(maker, name, price) { // コンストラクタの定義
    this.maker = maker; // プロパティの定義と代入
    this.name = name;
    this.price = price;
  }
  show() { // メソッドの定義functionは不要
    return `${this.maker}.${this.name}.${this.price}`
  }
}
let c = new Car('フェラーリー', 'LaFerrari', 13500000); // 生成
console.log(c.show()); // メソッドの呼び出し
```

---
### クラス定義 (2 / 6)
- class 内で直に変数を定義することはできない。関数内でのみ可能。
- constructor は重複できない。省略は可能。
- 関数などと違い、定義前の呼び出しは不可（hoistされない）

```JavaScript
class Car {
  constructor(){};
  constructor(){}; // 二重定義はNG
  this.a = 1; // NG: プロパティ代入はメソッドやコンストラクタの中で
  let b = 2 ; // NG;
  test(){
    this.a = 1; // OK
    let b= 2;  //OK
  }  
}
```

+++
### hoistとは？
- 巻き上げ: varやlet宣言されたものは、コードの先頭で宣言したものとして位置付けられるため、宣言前でも参照できること。
- 変数やクラスの宣言位置と参照位置の関係
 - 関数とは異なりクラスについては、hositできないことに留意

```JavaScript
// 定義前の呼び出しは利用不可
let c = new Car();
class Car {
  //....
}
```
---
### クラス定義 (3 / 6)
- クラスリテラル

```JavaScript
var Car = class { // 無名クラスの定義と変数への代入
  constructor(maker, name, price) {
    this.maker = maker;
    this.name = name;
    this.price =price;
  }
  show() { // メソッドの定義functionは不要
    return `${this.maker}.${this.name}.${this.price}`
  }
}
let c = new Car('フェラーリー', 'LaFerrari', 13500000); // 生成
```

---
### クラス定義 (4 / 6)
- static 修飾子

```ES6
class Car {
  static test(){ return 'static test';}
}
console.log(Car.test()); // staticは静的メソッド。インスタンスの生成なしに利用できる
```

---
### クラス定義 (5 / 6)
- アクセッサ: **get**, **set** 記述を追加することでプロパティの代入・参照時に処理を組み込ませることができる

```JavaScript
class Car {
  constructor(a) {
    this.a = a;
  }
  get b() {return this._b; }
  get b(v) { this._b = v; }
  show() { return `${this.a}:${this.b}`;}
}
let c = new Car('my car');
c.b = 'your car';
console.log(c.show()); // my car:your car
```


---
### クラス定義 (6 / 6)
- **extends** キーワードによるクラスの継承。差分プログラミングができる。

```JavaScript
class Car {
  constructor(maker, name) {
    this.maker = maker;
    this.name = name;
  }
  show() { return `${this.maker}.${this.name}`; }
}

class RacingCar extends Car { // Carを継承（拡張）
  constructor(maker, name, category) {
    super(maker, name);
    this.category = category;
  }
  show() { return `${super.show()}:${this.category}`; }
}
let c = newRacingCar('トヨタ', 'TS050 HYBRID', 'LMP1');
console.log(c.show());
```

---
### イテレーター (1 / 2)
- **for…of** 命令で列挙可能なオブジェクトを作成するためのオブジェクト
-  **Array、String、Map、Set** などの組み込みオブジェクトは、デフォルトでこのイテレータが組み込まれている

---
### イテレーター (2 / 2)
- next 関数を戻り値に持つ関数を、プロパティ **Symbol.iterator** に設定
- next 関数は、続きがあるかどうか(done)と、続きがあるならば、現在の値(value)を一緒に返す

+++

```JavaScript
class Test {
  constructor () {
    this[Symbol.iterator] = () => {
      let i = 0;
      return {
        next() {
          // 0-2まで繰り返す、3になったらdone:trueを返す
          return i < 3 ? {value: i++, done:false} : {done: true};
        }
      };
    };
  }
}
let test = new Test();
for (let v of c) console.log(v);
```

---
### ジェネレーター
- 列挙可能なオブジェクトの実装がより簡単になる
 - **function❇︎ ** キーワードで定義
 - **yield** 命令で値を返す

```JavaScript
class Test {
  constructor () {
    this[Symbol.iterator] = function *() {
      let i = 0;
      while(i < 3) yield i++;
    };
  }
}
let test = new Test();
for (let v of c) console.log(v);
```
---

### モジュール機能 (1 / 3)
- 関数やクラスをimport, exportキーワードを利用してモジュール登録と参照が可能

```JavaScript
// module.js
export var a = 1;
export let b = 2;
export function test1(){ return 'test1; '; }
export function test2(){ return 'test2; '; }
function test3() {return 'test3';}

// test.js
import {test1, test3, a, b} from './module.js';
console.log(test1());
console.log(test2());
console.log(test3());
console.log(a);
console.log(b);
```


---
### モジュール機能 (2 / 3)
- import構文
```JavaScript
import {name, …} from module
```
 - **name**：インポートする変数や関数
 - **module**：インポートするjsファイル
```JavaScript
import * as alias from module
```
 - **alias**：moduleの別名
 - **module**：インポートするjsファイル

---
### モジュール機能 (3 / 3)
- default キーワードにより、名前のいらないエクスポートを宣言できる
- Node.jsではそのままでは実行できない

```JavaScript
// module.js
export default function test1() { return 'test1'};
export function test2() { return 'test2'};

// test.js
import a from './test.js'; // デフォルトのみ取得
console.log(a());

```

---
### ブラウザでの実行準備
#### 一つのjsファイルに束ねる方法
- 以下コマンドを順に実行し、必要な機能をインストール

```bash
$ npm install -g --save-dev browserify
$ npm install --save-dev babelify
```

- 以下コマンドで、jsファイルを変換・結合し、ブラウザで実行可能な jsファイルを作成する

```
browserify <jsファイル1> <jsファイル2> -t
  [babelify --presets es2015] –o<ブラウザ用jsファイル>
```
---
### browserifyのコマンド例
```
browserify module.js test.js -t [babelify --presets es2015] -o bundle.js
```
- この後、Node.jsでもブラウザ上でも利用可能に

---
### 既存の組み込みオブジェクトに対する機能の拡充
-  String、Array、Math、Object などの組み込みオブジェクトに便利な関数が追加されている
- 参考Webサイト
 - [『Mozilla における ECMAScript 6 のサポート』](https://developer.mozilla.org/ja/docs/Web/JavaScript/ECMAScript_6_support_in_Mozilla)
