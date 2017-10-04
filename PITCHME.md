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
var f1 = function(a, b) { return a * b };

// 上記をアロー関数に置き換えたもの
var f2 = (a, b) => { return a * b };
console.log(f1(2,3)); // 6
console.log(f2(2,3)); // 6
```

---
### アロー関数②
#### thisキーワードの意味の違い
- thisの意味
 - 通常の関数f1内
	 - globalオブジェクト

```JavaScript
let MyObject = function MyObject() {
  this.i = 1;
  console.log(this); // オブジェクト自身の参照
  var f1 = function() {
    console.log(this);
    console.log(this.i); // undefined
  };
  f1();
```

+++
#### 続き

- thisの意味
- アロー関数f2内
  - testオブジェクト

```JavaScript
  var f2 = () => {
      console.log(this);
      console.log(this.i);
  };
  f2();
}

var myObject = new MyObject();
```


---
### 関数とnew 演算子
関数 → オブジェクトの一種
 new 関数名()
新しい関数オブジェクトを生成し、その生成されたオブジェクトを返す
new演算子にかかる関数は、コンストラクタの役割

---
### アロー関数③
省略記法 1

---
### アロー関数④
オブジェクトリテラルとデフォルト引数

---
### アロー関数⑤
可変長引数、分割代入、展開演算子

---
### Promiseオブジェクト①
非同期処理が連なって可読性が悪くなったコールバック連鎖を改善できる、非同期処理制御オブジェクト。


---
### コールバック関数とは
イベント等が発生した時に実行してほしい関数のこと。
すぐに処理が終了しない非同期通信などで使われる
処理が終了したら、あらかじめ登録したコールバック関数が呼び出される

---
### Promiseオブジェクト②
 Promiseオブジェクトを使用した例
入れ子になっていない
非同期処理を行う関数（test2）の戻り値をPromiseオブジェクトにする
非同期処理完了後、thenメソッドが呼ばれる


---
### Promiseオブジェクト③
Promiseコンストラクタの構文
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
