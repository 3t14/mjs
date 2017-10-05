#### モダンJavaScriptプログラミング入門
# 5. ES6の基本文法1
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
- アロー関数などの関数表現の改善

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
### データ型 Symbol (1 / 5)
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
### データ型Symbol (2 / 5)
- Symbolは、生成したあとに代入した変数や定数を保持しない限り、どこからも参照することができない
- Symbolは、オブジェクトのプロパティのキーとして利用可能（文字列ではないため）
 - Symbolをプロパティのキーとして利用することで、外部からの参照ができない。
- 従来はビルトインのオブジェクトですら、上書きできてしまった。

---
### データ型Symbol (3 / 5)
#### プライベートなプロパティとしての利用例

- プロパティのキーとして利用可能
- **for…in** イテレーションや **JSON.stringfy()** メソッドで出力されない


```JavaScript
let myObj = {};
myObj[Symbol("key1")] = "a";
myObj["key2"] = "b";
myObj["key3"] = "c";

for (var key in myObj) {
    console.log(myObj[key]); // "b" and "c"
}

console.log( JSON.stringify(myObj)); // {"key2": "b", "key3":"c"}
```

---
### データ型Symbol (4 / 5)
#### 定数としての利用例①

- 下記のようなコードの場合
 - 変数 *tmp* を定数 *A* と比較しようとすると、*A*・*C*・*0*(ゼロ)の３パターンで一致するため、バグの元となりやすい

```JavaScript
const A = 0;
const B = 1;
const C = 0;

var tmp = 0;

if (tmp === A) console.log("tmp = A");
if (tmp === 0) console.log("tmp = 0");
if (tmp === C) console.log("tmp = C");
if (tmp === B) console.log("tmp = B");
```

---
### データ型Symbol (5 / 5)
#### 定数としての利用例②

- **Symbol** を利用して定数を宣言すると、変数 *tmp* は定数 *A* としか一致させることができない

```JavaScript
const A = Symbol();
const B = Symbol();

let tmp = A;

if (tmp === A) console.log("tmp = A");
if (tmp === B) console.log("tmp = B");
```

---
### 分割代入 (1 / 3)

- 右辺の配列やオブジェクトの各要素・プロパティを、左辺の個々の変数に展開

```JavaScript
var [a, b, ...others] = [1, 2, 3, 4, 5];
console.log(a); // 1
console.log(b); // 2
console.log(c); //[3, 4, 5]

var {key1, key2} = {key1: 'value1', key2: 'value2'};
console.log(key1); // value1
console.log(key2); // value2
```

---
### 分割代入 (2 / 3)

#### 名前付き引数を指定

```JavaScript
function test({a = 1, b = 2}){
    return a * b;
}
console.log(test({a:3, b:4}));
```

#### 変数の値を入れ替える

```JavaScript
var [a, b] = [1, 2];
[a, b] = [b, a];
console.log(a); // 2
console.log(a); // 1
```

---
### 分割代入 (3 / 3)
#### 正規表現

```JavaScript
var text = "11-22";
var pattern = /^(.+)-(.+)$/;
var [a, b, c] = pattern.exec(text);
console.log(a); // 11-22
console.log(b); // 11
console.log(c); // 22
```
@[2](ハイフン区切りで分割)
@[3](分割した結果を代入)
@[4](第0要素は全ての文字列)
@[5](第1要素は分割後の最初の文字列)
@[6](第2要素は分割後の最後の文字列)


---
### 展開演算子
- 配列などを関数の引数や配列リテラル内で展開するための演算子
- 展開したいオブジェクトの前に“**…**”を記述する

```JavaScript
var args = [1, 2, 3];
// 関数の引数で利用したい場合
function test(a, b, c) { console.log( a + b + c); }
test.apply(null, args); // 6（従来の方法: 配列を引数として引き渡して実行）
test(...args); 		// 6 (ES6: 配列argsを展開して引数として割り当て実行)

// 配列リテラル内で利用したい場合
var args = [4, ...args, 5, 6];
console.log(args2); //4, 1, 2, 3, 5, 6
```

---
### for 〜 of 構文 (1 / 3)
#### **for 〜 in 構文** との違い
- **for 〜 in 構文**
 - オブジェクト内にある、すべての列挙可能(Enumerable)なプロパティを列挙
- **for 〜 of 構文**
 - 反復列挙可能(Iterable)なオブジェクトが持つ値のみを列挙

---
### for 〜 of 構文 (2 / 3)
#### 利用可能なデータ型
- 要素の反復列挙可能なビルトインデータ型
 - **Array**, **TypedArray**, **String**, **Map**, **Set**
- 要素の反復列挙不可能なビルトインデータ型
 - **Object**

---
### for 〜 of 構文 (3 / 3)
#### 参照する値の違い
- **for 〜 in 構文** は添字（インデックスやプロパティ名）を参照
- **for 〜 of 構文** は要素を参照

```JavaScript
var a = [1, 2, 3];
Array.prototype.key1 = "value1";
// for in
for (let key in a) console.log(key); // 0, 1, 2, key1

// for of
for (let elem of a) console.log(elem); // 1, 2, 3
```

---
## 引数のデフォルト値 (1 / 3)
 - 引数にデフォルト値を設定できるようになった
 - 他の引数を参照して使用することも可能


```JavaScript
function test(a = 1, b = 2) {
    return a * b;
}

console.log(test());	// 2
console.log(test(2, 3));	//6

function test2(a = 1, b = a) {
    return a * b;
}

console.log(test2());		// 1
console.log(test2(2));	// 4
```

---
## 引数のデフォルト値 (2 / 3)
 - デフォルト引数が設定されていなければ、**undefined** がデフォルト値になる

```JavaScript
function test3(a, b) { // ES6以前の対応方法
    a = typeof a !== 'undefined' ? a : 1; // 未定義なら1
    b = typeof b !== 'undefined' ? b : 1; // 未定義なら1
    return a * b;
}

console.log(test3());	// 2
console.log(test3(3));	// 6
```

---
## 引数のデフォルト値 (3 / 3)
 - **undefined** が指定された場合は、デフォルト引数が適用される
 - **null** や **false** が指定された場合は、デフォルト引数は無視される


```JavaScript
function test4(a = 1, b = 2) { // ES6以前の対応方法
    return a * b;
}

console.log(test4(2, undefined));		// 2
console.log(test4(2, null));	// 0
console.log(test4(2, false));	// 0 : falseも未定義として扱われる
```

---
## 可変長引数
 - **Array** オブジェクトとして扱われるため、**Array** の標準メソッドが利用可能
 - 従来の **arguments** オブジェクト
  - 引数オブジェクト
  - 配列と似ているが、配列操作ができない

```JavaScript
function test(...a){
    return a;
}
console.log(test(1,2,3)); // [1, 2, 3]

```

+++

```JavaScript
function test2(...a){
    a.push(4);
    return a;
}
console.log(test2(1,2,3)); // [1, 2, 3, 4]

function test3(a){
    return arguments;
}
console.log(test3(1,2,3)); // [1, 2, 3]

function test4(a){
    arguments.push(4); // NG
    return arguments;
}
console.log(test4(1,2,3)); // NG
```
