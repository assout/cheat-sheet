# Document format rules

Date: 2014-10-30 14:49
Tags: []
Categories: []

---

## 構成

- 言葉の定義
- 基本設計
    - 機能追加の目的
        - -> 現状の問題点など
    - 考慮すること
- 詳細設計
    - -> どう実現していくか
    - -> 細かい条件など
- 画面レイアウト設計

## フォーマット

- 説明資料は基本 PPT で作る
    - -> Excelは印刷に不向き
    - -> アウトラインレベルは markdown で書く

## Excel で作る場合

アウトラインがわかりやすいように以下の構成とする
markdown と互換性を持たせとくのはやめる。(Excelとしてみた時に見づらいため)

A1 : シートタイトル
B列: 空行
A列: 1. 章名
A列:   1.1. 節名

節以降もA列内でインデントする。

- インデント、章番号の作成は、RelaxToolsのRelaxWord機能を使う。(Refs: [microsoft-excel](microsoft-excel))
- 章題、節第、項題は下線を引く -> TODO: めんどくさい

## References

[create-note-rules](create-note-rules)

