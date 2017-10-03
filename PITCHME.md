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

- 外部JSファイルの記述例
```javascript
document.writeln('Hello, World!');
```

```HTML
<html>
<head>
</head>
<body>
<script type=“text/javascript” src="test.js" charset="utf-8">
</script>
</body>
</html>
```

@[5](script開始タグ)
@[5](srcにファイルパス)
@[5](charsetに文字コード)
@[5](空要素タグではなく、必ず終了タグを記述する)
@[9](HTMLタグは不要、指定された文字コードで作成)
