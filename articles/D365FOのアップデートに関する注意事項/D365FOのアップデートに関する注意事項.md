---
title: D365FOのアップデートに関する注意事項
date: 2022-03-04
tags:
  - Information

disableDisclaimer: false
---

こんにちは、Dynamics ERP サポートチームの今岡です。  
この記事では、Dynamics 365 Finance and Operations (D365FO) のアップデートに関する注意事項を紹介します。  
<!-- more -->

# 「サービスアップデート自動適用の一時停止」の注意点

D365FOのサービスアップデートにつきまして、以下のドキュメントに記載されていますように、  
最大3つまでの更新を続けて一時停止することができます。  

[更新を遅らせることができますか、ポリシーとは何ですか。](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/fin-ops/get-started/one-version#can-the-update-be-delayed-what-is-the-policy)

４回以上の一時停止は、**いかなる理由でも実施できません**のでご注意ください。  
本番環境は、サービス終了する前にアップデートして頂くことで、常にサポートされている環境を維持頂き  
何らかの理由で、サービス終了までにアップデートできなかった場合も、3つの一時停止の範囲内で最新のサービスアップデートをご適用ください。  
  
ただし、４回目のアップデート期日前に、本番環境に手動で最新サービスアップデートを適用した場合は、LCSから一時停止が可能となります。  
遅くとも自動適用予定日の１週間前には手動でご適用ください。  

# 「サービス終了」の期日

各サービスアップデートの「サービス終了」期日は以下のドキュメントでご確認頂けます。  
[サービス更新の可用性](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/fin-ops/get-started/public-preview-releases)

# サービス終了前にアップデートを適用するメリット

サービス終了前にアップデート頂くことで、常にサポートされている環境を維持でき、以下のようなメリットもございます。  
1. 問題発生時に調査及びトラブルシューティングを依頼可能です。  
2. Criticalな問題が発見された場合、新しいサービスアップデートを適用することなく、Quality Updateから修正を入手可能です。  
  
# 「サービス終了」した環境の制約
        
「サービス終了」した環境では多くの制約が発生しますのでご注意ください。  
1. Microsoft は、サービスの終了に達しているバージョンに対して、修正プログラムをリリースしません。  
2. 3つのサービス更新より古いバージョンで発生した問題の調査とトラブルシューティングを行いません。  
3. 以下のLCS機能が使用不可となる可能性がございます。  
    * メンテナンス モードの有効化  
    * 環境または環境間でデータベースを移動するために提供されるすべての機能を使用する  
    * SQL Server データベースへのファイアウォール アクセスの有効化  
    * RSAT 証明書のダウンロード  
    * RSAT 証明書を再生成する  
  
(参考URL)  
[サービスの終了にはどのような意味がありますか?](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/fin-ops/get-started/one-version#what-does-end-of-service-mean)  
[サポートされなくなった Finance and Operations バージョンを実行している環境はどうなりますか？](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/fin-ops/get-started/one-version#what-happens-to-an-environment-that-is-running-a-finance-and-operations-version-that-is-no-longer-supported)  


# おわりに  
  
より詳細な情報が必要な場合、弊社テクニカルサポート、Customer Success Account Manager (CSAM), Customer Engineer (CE) までお問い合わせください。  