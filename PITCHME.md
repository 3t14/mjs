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
### let命令（1 / 3）
- **if** や **for** などのブロック内(“**{}**”で囲まれた部分)でのみ有効な変数の宣言に使用。<br />
	→ **ブロックスコープ**
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

---
### let命令（2 / 3）
-  **switch** ブロック内で使用する場合は、全体で一つのブロックなので注意

```JavaScript
var num = 1;
switch (num) {
	case 0:
		let a = "num = 0 ";
		break;
	case 1:
		let a = "num = 1"; // NG
		break;
}
```
@[4](最初の宣言なのでOK)
@[7](2回目の宣言なのでNG)

---
### let命令（3 / 3）
-  任意のスコープを作る目的で **即時関数** を利用しない。
- ブロックで括り、letキーワードを使用することで同じ効果を得られる

```JavaScript
(function () {
	var a = 1;  // 即時関数内部での宣言
}());
console.log(a); // 変数aは見えない
// let　キーワードを利用した場合
{
	let b = 1;
}
console.log(b); // 変数bは見えない
```

+++
### 即時関数とは
- 即時実行される**無名関数**
- 無名関数の定義を括弧でくくることで、式の評価内部で関数定義を先に評価。”**()**”表記を追記することで、定義した無名関数をすぐに実行する。

- 書式
> (無名関数の定義)()

+++
### 即時関数を利用する理由
- スコープの変数汚染を防ぐ。
- 即時関数＝使い捨て→外部参照できない。

+++
### クロージャー
- 関数閉包ともいう。
 - 引数以外の変数を自身が定義された環境で解決することを特徴としたもの
- JavaScriptにおいて
 - 関数自身を戻り値とする関数
 - 外部参照不可能な変数の定義
 - 定義後にも、戻り値として返した関数内部から、外部参照不可能変数への参照が可能

+++?image=/assets/PITCHME-9f09d.png&size=contain

+++?gist=3t14/22a7948b4691a20fb0b42b14a19e9fa3&lang=JavaScript
#### クロージャと即時関数を用いたクラス定義の例

@[3](Symbolのキーにより外部参照が不可に)
@[14](secretPropKeyの変数は参照できない)
