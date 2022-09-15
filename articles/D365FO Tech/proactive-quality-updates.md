---
title: Dynamics 365 for Finance and Operations のプロアクティブな品質更新プログラムの適用について
date: 2022-09-15
tags:
  - D365FO
  - tips

disableDisclaimer: false
---

こんにちは、日本マイクロソフトのDynamics サポートチームです。
この記事では、 Dynamics 365 for Finance and Operations のプロアクティブな品質更新プログラムの適用についてご案内します。

品質更新プログラム (Quality update program) は修正プログラム (Hotfix) の累積的なものとなり、今まではお客様が手動でサンドボックス環境、本番環境に適用して頂く必要がございましたが、今後はマイクロソフトにより自動で適用致します。
こちらの変更は2022 年 9 月末または 10 月より段階的にサンドボックス環境に対して開始される予定となっており、2022 年 9 月中には対象環境のスケジュールに対してメールにて通知をさせて頂きます。

<!-- more -->
---

下記公開情報を基にご説明いたします。各項目について公開情報内にも詳細を記載しておりますのでご参照ください。
https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/get-started/quality-updates?context=%2Fdynamics365%2Fcontext%2Ffinance
https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/deployment/plannedmaintenance-selfservice#what-is-the-schedule-for-proactive-quality-updates

## 今まで
今までは、セキュリティ、プライバシー、信頼性、可用性、パフォーマンスなどの基本的な要素に対する修正プログラム (Hotfix) の累積である品質更新プログラム (Quality update program) は、LCS にて公開されるごとに、以下のブログの手順よりお客様が手動でサンドボックス環境、本番環境に適用して頂く必要がございました。
https://jpdynamicserp.github.io/blog/D365FO%20Tech/apply-quality-update-d365fo/
そのため、公開された品質更新プログラムを手動で適用していない環境では、修正プログラムにて対処されているはずの問題が発生するということが発生しておりました。

## 今後
今回の変更では、品質更新プログラムを自動でマイクロソフトにより環境に適用致します。これにより常に最新の修正を含んだ状態の環境をご利用して頂くことになり、より高い品質を提供することができます。
また、今までは、品質更新プログラムの手動適用の実績の有無により、例えば、同じバージョン10.0.28 の環境でも異なるビルド番号 (マイナーバージョン) の環境が混在していましたが、こちらの変更により基本的には10.0.28 の環境は全て同じビルド番号 (マイナーバージョン) となり、問題の発見とソリューションの提供が早くなります。


## 重要事項
品質更新プログラムの自動適用に関する重要事項を以下にまとめております。
1. **自動適用の対象の段階的な拡大**
まずは、2022 年 9 月末または 10 月より段階的にサンドボックス環境に対して開始される予定となっており、2022 年 9 月中にはスケジュールに対してメールにて通知をさせて頂きます。
正常に自動適用が完了していく環境の割合が増えたことを確認後、本番環境への自動適用が開始される予定です。
現時点では本番環境は2022 年 11 月以降に自動適用が開始される予定です。

2. **Near-zero downtime updating (ゼロに近いダウンタイム更新)**
以下の公開資料の最小限のダウンタイムで自動適用は実施されますので、自動適用時の影響は最小限なものとなります。
https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/deployment/plannedmaintenance-selfservice#what-does-near-zero-downtime-maintenance-mean
以下の公開資料の優先順位に基づくバッチ スケジューリングにより、自動適用の際のバッチジョブ実行を対策することができ、バッチのスケジューリングと処理は自動適用直後に復旧し、再開されます。 
https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/sysadmin/priority-based-batch-scheduling
https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/deployment/plannedmaintenance-selfservice#priority-based-scheduling

2. **自動適用スケジュールの公開**
以下の公開資料の通り、各リージョンごとに自動適用が実施される4 日間のウィンドウが決定され、5 営業日前にはメールにて通知いたします。そのウィンドウ内にて自動適用を実施致します。
https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/deployment/plannedmaintenance-selfservice#what-is-the-schedule-for-proactive-quality-updates


4. **Dark hours (暗い時間帯)**
以下の公開資料の通り、環境が配置されているリージョンごとに、深夜から早朝のDark hours (暗い時間帯、営業時間外)が定義されており、そのDark hours 内で自動適用が実施されますので、自動適用時の環境のご利用に対する影響は最小限となります。
日本リージョンは 1:00 AM ~ 7:00 AM (日本時間) となります。
https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/deployment/plannedmaintenance-selfservice#what-are-the-planned-maintenance-windows


また、以下の公開資料の下部にQ&Aがございますので、こちらもご確認して頂けますと幸いでございます。
https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/get-started/quality-updates?context=%2Fdynamics365%2Fcontext%2Ffinance

---
## おわりに  

以上、 Dynamics 365 for Finance and Operations のプロアクティブな品質更新プログラムの適用についてご紹介しました。
もし、お困りのこと等がございましたら、弊社までお問い合わせ頂きますようお願いいたします。
