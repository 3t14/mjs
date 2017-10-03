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
クロージャと即時関数を用いたクラス定義の例

@[3](Symbolのキーにより外部参照が不可に)
@[15](secretPropKeyの変数は参照できない)

---
### const命令
- 定数（再代入ができない変数）の宣言に使用
- **let** と同じく、スコープは **ブロック単位**

```JavaScript
if (true) {
	const constValue = "const";
	console.log(constValue);
	constValue = "const test"; // NG
}
console.log(constValue);

const constValue = [0, 2];
constValue[1] = 3;
console.log(constValue);
```
@[2, 7](定数宣言)
@[4](定数は再代入不可)
@[6](定数だとしても、ブロック外からの参照不可)
@[9](配列の要素は、定数ではない)

---
### 2進数・8進数リテラル
- 2進数と8進数のリテラルが新たに追加
- 2進数は「**0b** (ゼロビー)」、8進数は「**0o** (ゼロオー)」で始める。

```JavaScript
var binary      = 0b1100;   // 2進数 ES6
var octal       = 0o14;     // 8進数 ES6
var decimal     = 12;       // 10進数
var hex         = 0xc;      // 16進数
var octalOld    = 014;      // *非標準 8進数（従来）

console.log(binary);        // 12
console.log(octal);         // 12
console.log(decimal);       // 12
console.log(hex);           // 12
console.log(octalOld);      // 12
```

---
### テンプレート文字列
- 文字列リテラルに変数・改行を埋め込める手段
- 文字列リテラルを *バッククォート* “**`**”<br/>（**shift** + **@**）で囲む
- 改行はそのまま改行文字列を入力
- 変数は“**${…}**”で埋め込む

```JavaScript
var test = "テスト";
var literalString1 = "文字列\nリテラル" + test; //従来の記述
var literalString2 = `文字列
リテラル ${test}`; // 新しく追加された記述方法

console.log(literalString1);
console.log(literalString2);
```

---
### タグ付きテンプレート文字列 (1 / 2)
- 関数を使用して、テンプレート文字列の出力を調整できる

```JavaScript
function tag(strings, ...values) {
	return "Magazine " + strings[0] + "[" + values[0] + "],"
										 + strings[1] + "[" + values[1] + "]";
}

var title = "Automatic operation";
var category = "Car";

console.log(tag `Title ${title} Category ${category}`);
// Magazine Title [Automatic operation], Category [Car]
```

---
### タグ付きテンプレート文字列 (2 / 2)
- 関数tagの引数
 - **strings**: テンプレート文字列の領域以外を配列化したもの
 - **values**: テンプレート文字列を順番に配列化したもの
- 前ページの例
 - strings: ["Title ", " Category "]
 - values: ["Automatic operation", "Car"]

---
### データ型 Symbol (1 / 3)
- リテラルによる表現を持たない、新しいプリミティブ型
- インスタンスが固有で不変

```JavaScript
var sym1 = Symbol();
var sym2 = Symbol('foo');
var sym3 = Symbol('foo');
var sym4 = Symbol('foo2');
var sym5 = new Symbol(); // NG

console.log( typeof sym1 );	// symbol
console.log( sym2 === sym3); // false
console.log( sym4.toString() ); // Symbol(foo2)
```

@[1-4](Symbolはnew演算子を使わず宣言)
@[5](new演算子を用いたためエラー)
@[7](typeof:データ型を文字列で出力)
@[8](引数の文字列は識別子ではなく、デバッグ用)
@[8](同一の文字列を指定してもエラーが発生)
@[9](Symbol(宣言時の引数値)と出力される)

---
### データ型Symbol (2 / 3)
#### プライベートなプロパティとしての利用例

- プロパティのキーとして利用可能
- **for…in** イテレーションや **JSON.stringfy()** メソッドで出力されない


```JavaScript
var myObj = {};
myObj[Symbol("key1")] = "a";
myObj["key2"] = "b";
myObj["key3"] = "c";

for (var key in myObj) {
	console.log(myObj[key]); // "b" and "c"
}

console.log( JSON.stringify(myObj)); // {"key2": "b", "key3":"c"}
```
