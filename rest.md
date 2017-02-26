# REST (Representational State Transfer)

Date: 2016-06-30 19:10
Tags: []
Categories: []

---

## 概要

> WEBのアーキテクチャスタイル（設計思想）
>
> RESTはWebのアーキテクチャスタイル（設計思想）である。アーキテクチャスタイルは（マクロ）アーキテクチャパターンとも呼ばれ、複数のアーキテクチャに共通する性質、様式、作法あるいは流儀をさす言葉である。アーキテクチャスタイルの例には、MVC（Model-View-Controller）やパイプ＆フィルタ（Pipe and Filter）、イベントシステム（Event System）などがある。

Refs: [Webのアーキテクチャスタイル（設計思想） REST](http://kaihooo.com/rest/)

## 基本操作

- GET:リソースの取得。GETでのアクセスはリソースの内容に影響を与えない。
- POST:リソースの新規作成
- PUT:既存のリソースのアップデート
- DELETE:リソースの削除

Refs: [\[ThinkIT\] 第4回：アーキテクチャスタイル「REST」とは何か (1/2)](https://thinkit.co.jp/free/article/0609/8/4/)

PUTとPOSTについて

PUTは冪等であるべき。
以下のイメージとなる。

    PUT http://hoge/user/{userId}
    POST http://hoge/user/

## ガイドライン

Refs: [APIを設計する前に読みたいガイドラインまとめ | NTT Communications Developer Portal](https://developer.ntt.com/ja/blog/522676d0-7336-4139-b70a-ec6059e10cf3)

