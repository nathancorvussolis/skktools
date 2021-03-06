はじめに
========

skkdic-expr2 は、SKK 辞書のユーティリティです。標準の SKK 辞書ツールと
同等の機能を持ち、より高速に実行する事を目指しています。


コンパイル&インストール
=======================

## 必要なもの

skkdic-expr2 は GLIB-2.0 を使いますので、あらかじめインストールされてい
る必要があります。

また、pkg-config が GLIB-2.0 を正しく見付けられる事が前提です。

うまくいかない場合は PKG_CONFIG_PATH の設定を見直してください。
GLIB-2.0 が見付からない場合は skkdic-expr2 はコンパイルされません。

## 作り方

標準の SKK 辞書ツールと同じです。GLIB-2.0 が見付かっている場合は、

  ```
  $ ./configure; make
  ```

で、SKK 辞書ツールと一緒に、自動的に作られます。


プログラムの説明
================

skkdic-epxr2 は、複数の SKK 辞書をマージしたり、差分をとったり、共通す
る語を抜き出す事ができます。

## 例1: jisyo1 と jisyo2 をマージして、jisyo3 の内容を引いてから newjisyo に格納

  ```
  $ skkdic-expr2 jisyo1 + jisyo2 - jisyo3 > newjisyo
  ```

## 例2: 自分のユーザー辞書に含まれる新規登録語（L辞書に含まれない語）のうち、wrong 辞書に登録された候補を出力

  ```
  $ skkdic-expr2 ~/.skk-jisyo - SKK-JISYO.L ^ SKK-JISYO.wrong
  ```

skkdic-expr2 はソートされた結果を出力しますので、skkdic-sort を使う必要
はありません。

## 書式

    skkdic-expr2 [-o 出力ファイル] 辞書ファイル [[+-^] 辞書ファイル]...

## オプション

-o 出力ファイル

作業結果を標準出力に出す代わりに、指定されたファイルに書き込みます。

## 演算子

  - `+` ... 続く辞書ファイルの内容を、これまでの結果にマージします。

  - `-` ... 続く辞書ファイルの内容を、これまでの結果から引きます。

  - `^` ... 続く辞書ファイルの内容と、これまでの結果との共通集合を求めます。
    `&` ではなく `^` である事に注意。`^` を選んだ理由は、cap に少しは似てるからです。

## 注意点

  * 現時点では、ユーザー辞書に含まれる、送り仮名を含んだデータ（"[]" で
    括られたもの）は削除されます。skkdic-expr のデフォルトでの挙動
    （-O を指定しない）と同じです。

  * 二つの辞書をマージする際に、同じ語に違う注釈が付けられていた場合は、
    二つの注釈を "," でつないで格納します。


著者
====

福地健太郎 <fukuchi@users.sourceforge.net>
