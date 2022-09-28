---
title: Power BI.com integration と Power BI Embedded の違いについて
date: 2022-07-15
tags:
  - D365FO
  - Power BI.com integration
  - Power BI Embedded

disableDisclaimer: false
---

こんにちは、日本マイクロソフトの岡田です。
Dynamics 365 Finance and Operations (以下D365FO) では、Power BI レポートの形式でデータを表示、及び参照することが可能です。
D365FO のデータを Power BI レポートで表示、参照する機能は、主に2つございますが、この記事ではその2つの違いについてご紹介させていただきます。

<!-- more -->
## 検証に用いた製品・バージョン
Dynamics 365 Finance and Operations      
Application version: 10.0.26 
Platform version: PU50

D365FO のデータを Power BI レポートで表示、参照する機能は、Power BI.com integration と Power BI Embedded の2つがございます。その違いについて以下の表にまとめましたので、ご参考にして頂けますと幸いです。

||Power BI.com integration|Power BI Embedded   |
|:---|:---|:---|
| 概要 | Power BI レポート を PowerBI.com に配置します。<br>Power BI レポートをD365FO のダッシュボードに<br>追加したり、PowerBI.com から参照可能です。| Power BI レポートを D365FO 内部に配置し(*1)、<br>D365FO の機能の一部として提供します。  |
| 開発方法 | Odata フィード でデータを取得する場合、<br>Power BI Desktopもしくは PowerBI.com より行います。<br>Direct query の場合には Power BI Desktop より行います。| Power BI Desktop より行います。  |
| データ接続 | Odata フィードもしくは Direct Query より<br> Entity Store データベース(AxDW) に接続します。| Direct Query より Entity Store データベース(AxDW) に<br>接続します。  |
| ライセンス | PowerBI.com で Power BI レポートを<br>共有ワークスペースへ公開する必要があるため、<br>Power BI Pro のライセンス(*2)が必要になります。| D365FO の機能の一部として提供するので<br> Power BI Pro ライセンスは必要ありません。  |
| 制限事項 | 特になし| Tier2 以上の環境(*3)で使用できる機能となっております。  |

(*1) Power BI レポートを D365FO へデプロイする方法と致しましては、以下弊社公式資料をご確認頂けますと幸いです。
https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/analytics/add-analytics-tab-workspaces?toc=%2Ffin-and-ops%2Ftoc.json

(*2) PowerBI.com で、 Power BI レポートを共有ワークスペースへ公開しない場合、Power BI レポートを個人のワークスペースに<br>持っているユーザーでしか、D365FO 上で Power BI レポートを参照できません。<br>複数のユーザー間でレポートを参照されたい場合、Power BI レポートを共有ワークスペースへ公開する必要があります。<br>共有ワークスペースへのレポートの公開は、Power BI Pro のライセンスが必要となります。詳細は以下の弊社公式資料をご確認頂けますと幸いです。
https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-how-to-collaborate-distribute-dashboards-reports#share-dashboards-and-reports

(*3) Power BI Embedded は、Azure SQL DB で使用できる機能となっておりますので、DB が SQL server となっている Cloud-hosted 環境では使用できない機能となっております。

---
## おわりに  

Power BI.com integration と Power BI Embedded の違いについて、ご紹介させていただきました。ご不明な点やご質問等ございましたら、弊社サポートまでお問い合わせ頂きますようお願いいたします。
