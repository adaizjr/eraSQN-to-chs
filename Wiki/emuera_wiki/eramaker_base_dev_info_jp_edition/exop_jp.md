﻿# 演算

----------------------------------------

+ 演算子
+ 暫定的な演算子の優先度表
+ 演算の追加
+ 論理演算子の短絡評価

----------------------------------------

## 演算子

### 単項演算子

+ `~`ビットごとの否定(ビットごとのNOT) 単項演算子（優先度最大）

+ `!`論理否定(NOT) 単項演算子（優先度最大）

### 二項演算子

+ `<<`左ビットシフト。比較やビット演算より優先度が高く、四則演算より低い。

+ `>>`右ビットシフト。比較やビット演算より優先度が高く、四則演算より低い。

+ `^`ビットごとの排他論理和(ビットごとのXOR) 優先度は&、`|`と同じ

+ `^^`ビットによらない排他論理和(ビットによらないXOR) 優先度は&&、`||`と同じ

+ `!&`ビットによらない否定論理積(ビットによらないNAND) 優先度は&&、`||`と同じ

+ `!|`ビットによらない否定論理和(ビットによらないNOR) 優先度は&&、`||`と同じ

### 三項演算子

+ `?～#`普通の三項演算子 優先度は=の上で他の演算子より下（判定および結果を先にまとめてから処理される）

	書式（数値）　：`<代入先変数> = <条件式> ? <真の場合の代入値> # <偽の場合の代入値>`

	書式（文字列）：`<代入先変数> = \@<条件式> ? <真の場合の代入値> # <偽の場合の代入値>\@`

	処理的には

	```
	IF <条件式>
	　　<代入先変数> = <真の場合の代入値>
	ELSE
	　　<代入先変数> = <偽の場合の代入値>
	ENDIF
	```

	と同じになります。

	なお、数値の三項演算子については、()の中に入れることにより、通常の計算の中で使うこともできますし、文字列の三項演算子については、そのままPRINTFORM系命令に使うことができます。

	ただし、\@～\@形式の三項演算子では#を省略することはできません。

### 代入演算子

+ `'=`文字列式を用いた文字列型変数への代入を行う演算子 詳しくは[こちら](/Wiki/emuera_wiki/eramaker_base_dev_info_jp_edition/exetc_jp.md#文字列式を用いた文字列変数への代入)。

### インクリメント・デクリメント

+ `++`インクリメント

+ `--`デクリメント

	代入文の代わりに使います。他の演算子と組み合わせることはできません。

----------------------------------------

## 暫定的な演算子の優先度表

|分類|優先度|代入複合演算|記号|
|----|----|----|----|
|否定演算子|高|×|`~`, `!`|
|算術演算子|↑|○|`*`, `/`, `%`|
|||○|`+`, `-`|
|ビットシフト演算子	||○|`<<`, `>>`|
|比較演算子||×|`<`, `>`, `<=`, `>=`|
|||×|`==`, `!=`|
|論理演算子||○|`&`, `\|`, `^`|
||↓|×|`&&`, `!&`, `\|?\|`, `!\|`, `^^`|
|三項演算子|低|×|`～?…#＿`|

----------------------------------------

## 演算の追加

+ `==` 文字列同士の比較。数値と文字列を比較することはできません。

+ `!=`文字列同士の比較。

+ `<`文字列同士の比較。比較は先頭から行われ、異なる文字が見つかった時点で決定されます。

+ `>`文字列同士の比較。

+ `<=`文字列同士の比較。

+ `>=`文字列同士の比較。

+ `+`文字列同士の連結。数値と文字列を加算・連結することはできません。

+ `*`文字列と整数の乗算。文字列と文字列を乗算することはできません。

```
STR:0 = % "あ" * 10 %
PRINTFORML STR:0 = "%STR:0%"
WAIT
;結果
STR:0 = "ああああああああああ"
```

----------------------------------------

## 論理演算子の短絡評価

短絡評価とはたとえば(X && Y)という式でXが0である時、Yの値によらず演算結果が0になることが明らかなのでYを評価しない、という評価法です。

吉里吉里を含む多くの言語では論理演算子を短絡評価します。

この評価法により以下のような書き方ができます。

```
IF (ASSI >= 0) && (NO:ASSI == 1)
	～～～
ELSE
	～～～
ENDIF
```

ASSIが0以下の場合、(NO:ASSI == 1)の結果によらず全体の結果は0なのでNO:ASSIは参照されません。 したがってエラーも発生しません。

評価順は左項が先、右項が後です。

```
　IF (NO:ASSI == 1) && (ASSI >= 0)
```

このように書くと先に(NO:ASSI == 1)を計算しようとするのでASSI < 0のときエラーになります。
