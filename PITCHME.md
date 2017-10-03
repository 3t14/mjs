#### モダンJavaScriptプログラミング入門
# 3. JavaScript / ES6の開発環境
#### 田中　充
##### 株式会社イワテシガ

Web教材: http://mj.is-good.net


---
## 従来の開発環境の問題点
- JavaScript＝JavaScriptエンジン上でコンパイルせずに動作するもの
- ブラウザ（≒フロントエンド)上で実行するのみ
 - HTML内もしくはJavaScriptファイルに記述するだけ
- モジュールの構成管理に対応していなかった。
 - モジュール間の依存関係が不明
 - メンテナンスしづらい問題が発生

---

## CommonJSの登場
- ブラウザ以外のJavaScriptの仕様を策定するためのプロジェクト
- 当初はサーバーのみを対象として検討していたためServerJSと命名されたが、その後、より広くを対象する方針にしたためCommonJSに改名
- 仕様の内容
 - Modules
 - Packages
 - Promises
 - Systemなど

---
### CommonJSにおけるモジュールの定義と利用例

```JavaScript
// math.js
module.exports.add = function() {
  var sum = 0, i = 0, args = arguments, l = args.length;
  while (i < l) {
    sum += args[i++];
  }
  return sum;
};

// increment.js: math.jsファイルのモジュールaddを取得
var = add = require('math').add;
// increment関数をモジュールとして出力
exports.increment = function(val) {
  return add(val, 1);
};

// to be continued
```
@[2](add関数を外部に公開)
@[11](math.jsファイルのadd関数を参照)
+++

### CommonJSにおけるモジュールの定義と利用例

```JavaScript

// main.js:
//  increment.jsで定義されたincrement関数をinc関数として採用
var inc = require('increment').increment;
var a = 1;
inc(a);

// end
```
@[4](increment.jsファイルのincrement関数を参照)

---
## Node.jsの登場

- Node.jsはUnixプラットフォーム上で動作するサーバーサイドのJavaScript実行環境
- 2009年にRyan Dahl氏によって開発
- JavaScriptエンジンはGoogle V8を利用
- Node.jsでは、CommonJSのモジュール機能等の一部仕様を採用
- 現在はWebSocketやIoTのスクリプト言語やその他の目的で広く利用
- パッケージ管理コマンドであるnpmは、JavaScriptのパッケージ管理ソフトとして広く普及

---
## JavaScriptのモダンな開発環境

- サーバーサイドJavaScript実行環境であるNode.jsを活用することが一般的
 - npmコマンドによるJavaScriptライブラリのパッケージ管理
 - npmコマンドが使えれば、altJSやSassやLESSなどのCSSプリプロセッサ、さらにはトランスパイラ環境も導入が容易！

---
## 当研修で利用する統合開発環境: Cloud9 https://c9.io

- クラウド統合開発環境<br /> <em>“Development As A Service”
(PaaS型の開発環境を提供）</em>
- ソースコードを公開してもよいのであれば、無料で無制限のワークスペースの利用が可能
- Sublime風のタブテキスト編集環境の利用が可能
- 言語に応じたコード補完機能を提供

---
## 利用可能なワークスペースのテンプレート
![](assets/PITCHME-ad0c9.png)

---
## Cloud9の料金体系
<div align="center">
<img src="assets/PITCHME-7bfc0.png" width="80%"/>
<br />
https://c9.io/pricing
</div>


---
## cloud9の利用登録（通常）
1. https://c9.io にアクセス
1. メールアドレスを入力し、[Sign Up]をクリック
1. 名前、ユーザ名などの情報を入力して[Create Account]ボタンをクリック

![](assets/PITCHME-afaf4.png)

---
## Cloud9の利用登録（当研修）
1. Webアンケートに入力したメールアドレスに、Cloud9の招待メールが送信される
1. 受信したメールのリンクをクリック
1. あとは、通常のユーザー登録とほぼ同様

<div align="center">
<img src="assets/PITCHME-6af44.png" width="70%" />
</div>
