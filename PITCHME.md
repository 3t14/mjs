#### モダンJavaScriptプログラミング入門
# 5. ES6の基本文法
#### 田中　充
##### 株式会社イワテシガ

Web教材: http://mj.is-good.net

---
### ES6の新たな仕様 (1 / 2)
- let / const 命令
- 2進数と8進数リテラル
- テンプレート文字列とタグ付きテンプレート文字
- Symbol型
- 分割代入
- 展開演算子
- for…of 命令
- 関数構文の改善

+++
### ES6の新たな仕様 (2 / 2)
- Promise、コレクション、Proxyオブジェクト
- class 命令
- イテレーター・ジェネレータ
- import・export 命令

---
## let命令（1 / 3）
- ifやforなどのブロック内(“{}”で囲まれた部分)でのみ有効な変数の宣言に使用。<br />
	→ ブロックスコープ
- 今まではブロックスコープの概念が無かった。（varによる宣言は関数内か外かの区別のみ）

```JavaScript
if (true) {
	var varValue = "varValue";
	let letValue = "letValue";

	console.log(varValue); // OK
	console.log(letValue); // OK
}

console.log(varValue); // OK
console.log(letValue); // NG
```
