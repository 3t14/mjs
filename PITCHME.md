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
console.log(f1(2,3)); // 6
console.log(f2(2,3)); // 6
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

入れ子になっていない
非同期処理を行う関数（test2）の戻り値をPromiseオブジェクトにする
非同期処理完了後、thenメソッドが呼ばれる


---
### Promiseオブジェクト③
- Promiseコンストラクタの構文
new Promise((resolve,reject)=>{時間のかかる処理を記述…})
 resolve：処理成功時に呼び出す関数
 reject：処理失敗時に呼び出す関数
thenメソッドの構文
then(onFullFilled,onRejected)
 onFullFilled：処理成功時のコールバック関数
 onRejected：処理失敗時のコールバック関数



---
### Promiseオブジェクト④
処理失敗時のコールバック関数は、一つにまとめることが可能

---
### Promiseオブジェクト⑤

---
### Promiseオブジェクト⑥
catch関数の利用
catch(reject)
reject：処理失敗時のコールバック関数

---
### Promiseオブジェクト⑦
 Promise.all関数を利用すると、複数の処理を並行に実行し、全て成功した場合に処理を行う、といったことも可能
その場合、受け取る値は配列となる

---
### Promiseオブジェクト⑧
 Promise.race関数では、一番最初に完了した処理の結果を元に、then関数が実行される

---
### Promiseオブジェクトの処理の流れ

---
### Proxyオブジェクト①
プロパティの設定・取得・削除・列挙など、基本的な操作をトラップし、カスタマイズするためのオブジェクト

---
### Proxyオブジェクト②
その他の主なトラップの例


---
### Proxyオブジェクト③
全てのトラップについては以下Webサイトを参照
『ECMAScript® 2016 Language Specification』
http://www.ecma-international.org/ecma-262/7.0/#sec-proxy-object-internal-methods-and-internal-slots
2015版ではトラップ“enumerate” が定義されていたが、2016版では削除されており、ChromeやFirefoxの最新版でも既に削除されているので注意

---
### Mapオブジェクト①
キーと値でデータを管理するオブジェクト
コレクションとして使う

---
### Mapオブジェクト②
従来は Object を使用してコレクションを作成していた。
 Object と Map の違い
 Object はデフォルトで特定のキーが作られる。Map には作られない。
 ※Object.create(null) を使うことで回避可能
 Object のキーは文字列のみ。Map は任意の値が可能。
 Object はサイズを取得できない。Map は簡単に取得可能。
 Map の各要素は、for...of ループで挿入順に取得可能。
---
### Setオブジェクト①
一意な値を格納するオブジェクト
同じ値を格納しようとしても無視される
参照型に注意
func と ()=>{} は別の値

---
### Setオブジェクト②
コンストラクターに配列を渡すと、要素が展開されて、別々の値として格納される
同じ値は無視される
---
### クラス定義①
JavaやC#などの言語と同じようにクラスを定義

---
### クラス定義②
hoistとは？

---
### クラス定義③
クラスリテラル

---
### クラス定義④
 static 修飾子
---
### クラス定義⑤
 extends キーワードによるクラスの継承

---
### クラス定義⑥
 Array、Dateなどの組み込みオブジェクトも継承可能
右図は Array オブジェクトの sort 関数をカスタマイズした例

---
### イテレーター①
 for…of 命令で列挙可能なオブジェクトを作成するためのオブジェクト
 Array、String、Map、Set などの組み込みオブジェクトは、デフォルトでこのイテレータが組み込まれている

---
### イテレーター②
 next 関数を戻り値に持つ関数を、プロパティ Symbol.iterator に設定
 next 関数は、続きがあるかどうか(done)と、続きがあるならば、現在の値(value)を一緒に返す

---
### ジェネレーター①
列挙可能なオブジェクトの実装がより簡単になる
 function* キーワードで定義
 yield 命令で値を返す

---
### モジュール機能①
関数やクラスをimport, exportキーワードを利用してモジュール登録と参照が可能

---
### モジュール機能②
import構文
import {name, …} from module
name：インポートする変数や関数
module：インポートするjsファイル
import * as alias from module
alias：moduleの別名
module：インポートするjsファイル


---
### モジュール機能③
 default キーワードにより、名前のいらないエクスポートを宣言できる

---
### ブラウザでの実行準備
#### 一つのjsファイルに束ねる方法
 以下コマンドを順に実行し、必要な機能をインストール
$ npm install –-save-dev browserify
$ npm install --save-dev babelify

以下コマンドで、jsファイルを変換・結合し、ブラウザで実行可能な jsファイルを作成する
browserify <jsファイル1> <jsファイル2> -t [babelify --presets es2015] –o<ブラウザ用jsファイル>

---
### 既存の組み込みオブジェクトに対する機能の拡充
 String、Array、Math、Object などの組み込みオブジェクトに便利な関数が追加されている
参考Webサイト
『Mozilla における ECMAScript 6 のサポート』https://developer.mozilla.org/ja/docs/Web/JavaScript/ECMAScript_6_support_in_Mozilla
