---
title: テーブルブラウザへのアクセス方法
date: 2022-07-01 
tags:
  - category
  - sub-category
  - sub-category
---

こんにちは、日本マイクロソフトの西田です。

この記事では、Webブラウザからテーブルを参照する「テーブルブラウザ」の利用手順をご紹介します。

<!-- more -->

## 手順 (例：CustTableにアクセスする場合)
1. URL「dynamics.com/」の後に次の文字列を追加し、Enterを押します。

    ?mi=SysTableBrowser&TableName=[テーブル名]&cmp=[法人名]&lng=[英語...en-us/日本語...ja]&limitednav=true

    例:会社「USMF」について
    ?mi=SysTableBrowser&TableName=CustTable&cmp=USMF&lng=en-us&limitednav=true

    ![](./table-browser-access/step1.png)

2. テーブルブラウザが表示されます。
   なお、Tier2以上の環境ではテーブルブラウザからレコードの追加・削除を行うことはできません。

   ![](./table-browser-access/step2.png)

## おわりに
---
以上、テーブルブラウザの利用手順についてご紹介いたしました。
