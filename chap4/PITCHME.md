#### モダンJavaScriptプログラミング入門
# 4. JavaScriptの基本文法
#### 田中　充
##### 株式会社イワテシガ

Web教材: http://mj.is-good.net


---
### HTML内部でのJSの組み込み方
#### "Hello, World!"出力の記述例

```HTML
<html>
<head>
</head>
<body>
<script type=“text/javascript”>
<!--
	document.writeln(‘Hello, World!’);
//-->
</script>
<noscript>JavaScriptは利用できません</noscript>
</body>
</html>
```
@[5, 9](scriptタグ、scriptの種類をtype属性に記入)
@[6-8](scriptタグ未対応ブラウザのためにコメントアウト)
@[6-8](その中にJSを記述)
@[7](body内部にHello, World+改行コードを動的に出力)
@[10](JSが利用できないブラウザ上で出力される内容)

---
### 外部JSファイルの組み込み方
#### "Hello, World!"出力の記述例


```HTML
// 外部JSファイルの記述例: test.js
document.writeln('Hello, World!');

// HTMLファイルの記述例
<html>
<head>
</head>
<body>
<script type=“text/javascript” src="test.js" charset="utf-8">
</script>
</body>
</html>
```

@[1-2](HTMLタグは不要、指定された文字コードで作成)

@[9](scriptタグ)
@[9](srcにファイルパス)
@[9](charsetに文字コード)
@[9](空要素タグではなく、必ず終了タグを記述する)

---
### HTMLタグでのJavaScriptの記述方法
#### URLとしての記述
- URLの先頭に**JavaScript:** と記述することで、その後にJSコードの埋め込みができる
```HTML
<a href="JavaScript:alert('Hello, World');">
ダイアログを表示
</a>
```
@[1, 3](リンクをクリックするとダイアログが表示)

---

### HTMLタグでのJavaScriptの記述方法
#### イベント属性での記述
- *img* タグの **onlcick属性** など**on + イベント名** のイベント属性に記述する場合は、**JavaScript:** を記述する必要はない

```HTML
<img　src="sample.png"　onclick="alert('Hello, World');" />
```


---
### HTMLへの文字列の動的出力

#### 例1: **docuement.write** で文字列を出力する

```JavaScript
document.write('Hello, World!<br/>');
document.write('こんにちは！');
```


#### HTMLソース

```HTML
Hello, World!<br />こんにちは！
```

---
### HTMLへの文字列の動的出力

#### 例2: **docuement.writeln** で文字列を出力する

```JavaScript
document.writeln('Hello, World!<br/>');
document.writeln('こんにちは！');
```
#### HTMLソース

```HTML
Hello, World!<br />
こんにちは！
```
@[0]()
@[1,2](writeln関数を用いると)
@[3,4](改行コードが加わる)


---
### コメントの記述例

#### 例1: インラインコメント（1行ずつのコメント）

```JavaScript
//コメントを記入
document.write(‘Hello, World!’); //ここでも可　
```
#### 例2: 複数行コメント

```JavaScript
/*
作成日：2017-10-04
作成者：山田 太郎
*/
```
---

### alertダイアログ

#### 例："Hello, World!"のダイアログ表示
- HTMLタグ属性への記述例
```HTML
<a href="JavaScript:alert('Hello, World');">
ダイアログを表示
</a>
```
 - 上記の描画結果
> <a href="JavaScript:alert('Hello, World');">
ダイアログを表示
</a>

- JavaScriptファイルなどでの記述例
```JavaScript
alert('Hello, World');
```

### JavaScriptでの文字列表記
- 一般的に、シングルクォーテーションの利用を推奨
 - Google JavaScript Style Guide: http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Strings#Strings
- 理由
 - 要素の属性に代入する際、ダブルクォーテーションを利用すると、正しくタグの解析ができなくなるため。

---

### ブラウザコンソール
- モダンなブラウザには、通常**デベロッパーツール** 機能が搭載されており、その中に**Console**の機能が含まれている。
 - Chrome, Edge, Firefox...
- 様々なログ出力や、動作確認、デバッグに利用可能

+++
#### Firefoxのコンソール起動方法
1. メニューボタンをクリック
1. 開発ツールをクリック
1. ウェブコンソールをクリック

<div align="center">
<img src="/assets/PITCHME-e595a.png" width="50%" />
</div>

+++
#### Chromeのコンソール起動方法
1. メニューボタンをクリック
1. 開発ツールをクリック
1. ウェブコンソールをクリック

<div align="center">
<img src="/assets/PITCHME-78447.png" width="50%" />
</div>

---
### ログ出力
#### console.log関数
- ブラウザコンソールへ文字列を出力する
- 文字列ではなくオブジェクトを引数に与えると、ツリーでオブジェクトの中身が出力される
- 記述例

```html
<script type="text/javascript">
<!–
	console.log("Hello world");
//-->
</script>
```

---
### 変数
- 数値や文字列を一時的に保管しておくための入れ物に名前を付けておき、その名前によって数値や文字列を参照できる。

```JavaScript
var word;
var cat;
var a, b; // カンマ区切りで複数の変数を同時に宣言
var i = 123; // iを宣言し、初期値123を代入
```


---
### データ型

- プリミティブ値
 - 不変(immutable)な値として定義されるデータ型
 - 文字列型であるstringもプリミティブ値であることに注意
- オブジェクト
 - プロパティのセット
 - プロパティは、追加削除可能

　
 <div style="font-size: 20pt">
 参考: https://developer.mozilla.org/ja/docs/Web/JavaScript/Data_structures
 </div>

---
### プリミティブ型
![](/assets/PITCHME-b7ed0.png)

<div style="font-size: 20pt">
参考: https://developer.mozilla.org/ja/docs/Web/JavaScript/Data_structures
</div>

---
### オブジェクト型
![](/assets/PITCHME-8234f.png)

<div style="font-size: 20pt">
参考: https://developer.mozilla.org/ja/docs/Web/JavaScript/Data_structures
</div>
---

### 代入演算子
- 変数に数値や文字列を格納することを代入と呼び、代入を行う際に記述す る“**=**” を **代入演算子** と呼ぶ。

- 記述例

```JavaScript
word = “Hello, World!”;
dog = 3;
cat = 0.44;
```

---
### 配列
- 複数の数値や文字列を扱うためのデータ構造

- 記述例
```JavaScript
var array1 = [1, 2, 3, 4, 5];
var array2 = [“a”, “b”, “c”, “d”];
```

---

### オブジェクト(連想配列)
- **キー** に関連付けてデータを格納するデータ構造
- **値** として **無名関数** を割り当てた場合、**関数（メソッド）** として利用可能

- 記述例
```JavaScript
var object1 = {“apple”:1, “melon”:3, “orange”:2};
var object2 = {“firstname”: “taro”, “lastname”:”yamada”};
```


---
### 比較演算子
- 2つの値について、等しい・大小や文字列の一致などの比較を行い、成立した場合は **真（True）** 、成立しない場合は **偽（False）** となる
- 条件文や繰り返し構文において、条件式として用いる

---

### 比較演算子の種別
|判定内容|演算子|
|:---:|:---:|
|等しい|==|
|等しくない|!=|
|より大きい|>|
|より大きいまたは等しい(以上)|>=|
|より小さい|<|
|より小さいまたは等しい(以下)|<=|
```
