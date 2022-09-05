---
title: Dynamics 365 for Finance and Operations の環境ごとの違い
date: 2022-09-05
tags:
  - D365FO
  - tips

disableDisclaimer: false
---

こんにちは、日本マイクロソフトの福原です。
この記事では、 Dynamics 365 for Finance and Operations (D365FO) の環境ごとの違いについてご案内します。
クラウドホスト環境、サンドボックス環境、Tier2環境、本番環境等、様々な呼び方の環境があり、また、それぞれの環境で使える機能も異なるので、分かりづらいというお声をいただくことがありますので、そのような場合には本記事をご参考ください。

<!-- more -->




| 環境名                         | 本番環境                 | サンドボックス環境                       | クラウドホスト環境                               | 
| :----------------------------- | :----------------------- | :--------------------------------------- | :----------------------------------------------- | 
| 配置可能なLCSプロジェクト                 | 実装プロジェクト         | 実装プロジェクト                         | 実装プロジェクト<br>  or パートナー試用版プロジェクト | 
| 呼ばれ方例                   | Production 環境、<br> 運用環境、 <br> Microsoft-managed 環境  | Sandbox環境、<br> Tier2~Tier5環境、非運用環境、 <br> Microsoft-managed 環境   | Cloud-hosted環境、<br> 開発環境、Tier1環境            | 
| 配置場所                       | Azure                    | Azure                                    | Azure                                            | 
| Azure Subscription (*1)             | Microsoft                | Microsoft                                | 顧客                                             | 
| データベース                   | Azure SQL                | Azure SQL                                | Azure VM 内のオンプレミスSQL Server              | 
| SSMSによる<br> データベースへの接続 | 不可                     | 可 (*2)                                       | 可                                               | 
| RDP接続                        | 不可                     | 不可                                     | 可                                               | 

(*1): 本番環境、サンドボックス環境は、Microsoft内のAzure Subscriptionに紐づいて管理されているので、顧客はAzure portalにて環境の情報を見ることができません。クラウドホスト環境は顧客のAzure Subscirption内で構築されますので、Azure portalにて環境や請求の情報を見ることができます。
(*2): https://jpdynamicserp.github.io/blog/D365FO%20Tech/database-just-in-time-jit-access/ の手順となります。

(*): 本記事は2022年9月1日の情報です。


---
## おわりに  

以上、 Dynamics 365 for Finance and Operations (D365FO) の環境ごとの違いについてご紹介しました。
もし、お困りのこと等がございましたら、弊社までお問い合わせ頂きますようお願いいたします。
