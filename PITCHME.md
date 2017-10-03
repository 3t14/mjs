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
例1: **docuement.write** で文字列を記述する場合

```JavaScript
document.write('Hello, World!<br/>');
document.write('こんにちは！');
```

- HTMLソースは？|

``Hello, World!<br />こんにちは！``|
