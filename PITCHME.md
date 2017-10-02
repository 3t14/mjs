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
#### CommonJSにおけるモジュールの定義と利用例

```JavaScript

module.exports.add = function() {
  var sum = 0, i = 0, args = arguments, l = args.length;
  while (i < l) {
    sum += args[i++];
  }
  return sum;
};

// increment.js // math.jsファイルのモジュールaddを取得
var = add = require('math').add;
// increment関数をモジュールとして出力
exports.increment = function(val) {
  return add(val, 1);
};

```
+++

#### CommonJSにおけるモジュールの定義と利用例

```JavaScript
// main.js
// increment.jsで定義されたincrement関数をinc関数として採用
var inc = require('increment').increment;
var a = 1;
inc(a);
```
----
