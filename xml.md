# XML

Date: 2016-08-15 00:44
Tags: []
Categories: []

---

## スタイルガイド

Refs:

- IBM: [Principles of XML design: When to use elements versus attributes](http://www.ibm.com/developerworks/library/x-eleatt/)
- Google:
    - [www.textdrop.net/google-styleguide-ja/xmlstyle.html](http://www.textdrop.net/google-styleguide-ja/xmlstyle.html)
    - [https://google.github.io/styleguide/xmlstyle.html](https://google.github.io/styleguide/xmlstyle.html)

## 要素・属性・値の使い分け

要素に向いているケース

- データが複数回出現するなら要素を使う。「data1=".." data2=".."」のようにはしない。
- 一つのオブジェクトとしてまとめることができ、親子関係があるなら要素を使う。
- 出現順序に意味がある場合
- 複数行のデータ
- データが巨大な場合や BASE64 変換されたバイナリなど。
- 内容が自然言語であれば要素に入れ、属性として使用言語を記述するのが良い。

属性に向いているケース

- 管理用のIDやコード番号は属性にする。
- 別のデータのクラス、役割、処理方法を表すメタデータの場合。
- 上書きされない限り子孫要素にも属性の内容が反映される場合（xml:lang や 名前空間宣言など）

値の記述

- key-value で表すことのできるデータは要素名としてキー、属性 value として value を記述するのが良いとされています。

Refs: [\[XML\]要素・属性の使い分けと命名規則（要素名・属性名の決め方） | PHP Archive](http://php-archive.net/php/xml-element-or-attribute/)
