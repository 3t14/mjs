#### モダンJavaScriptプログラミング入門
# 4. JavaScriptの基本文法
#### 田中　充
##### 株式会社イワテシガ

Web教材: http://mj.is-good.net


---
## HTML内部におけるJavaScriptの組み込み方
### "Hello, World!"出力の記述例

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
@[6,8](scriptタグに対応していないブラウザのためにコメントアウトの中にJSを記述)
@[7](body部内部にHello, Worldを改行コードを付与して動的に出力)
@[10](JavaScriptが利用できないブラウザ上で出力される内容)

---
