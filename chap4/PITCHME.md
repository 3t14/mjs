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

<div align="center">
<img src="/assets/PITCHME-2caaa.png" width="50%" />
</div>
