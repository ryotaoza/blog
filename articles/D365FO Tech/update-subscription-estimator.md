---
title: Dynamics 365 for Finance and Operations の本番環境を使用するユーザー数が増えた場合の注意事項
date: 2022-05-09
tags:
  - D365FO
  - tips

disableDisclaimer: false
---

こんにちは、日本マイクロソフトの福原です。
この記事では、 Dynamics 365 for Finance and Operations の本番環境を使用するユーザー数が増えた場合の注意事項についてご案内致します。
<!-- more -->


本番環境を構築する際には、その時点での購入済みライセンス数、見込まれるトランザクション量をLCSのサブスクリプション試算(Subscription estimator)に登録することで、ライセンス数(ユーザー数)、トランザクション量に見合った本番環境のスペックがシステムにより決まり、そのスペックで本番環境は構築されます。

**本番環境の構築後、追加のライセンスの購入等により、ライセンス数、見込まれるトランザクション量が増えましても、ライセンス数、見込まれるトランザクション量はサブスクリプション試算(Subscription estimator)に自動で反映されないものとなっておりますことをご注意して頂きますようお願い致します。**
**ユーザー数が増えた場合にはサブスクリプション試算(Subscription estimator)を再度登録して頂きますようお願い致します。**`
再度、LCSにてサブスクリプション試算(Subscription estimator)を登録して頂くことで、変更後のライセンス数、見込まれるトランザクション量に見合うスペックが再度決定され、場合によりましては本番環境のスペックが良くなることがございます。


サブスクリプション試算(Subscription estimator)のご利用手順につきましては以下の弊社公開資料をご確認頂きますようお願い致します。
https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/lifecycle-services/subscription-estimator


---
## おわりに  

以上、 Dynamics 365 for Finance and Operations の本番環境を使用するユーザー数が増えた場合の注意事項についてご紹介させていただきました。
もし、お困りのこと等がございましたら、弊社までお問い合わせ頂きますようお願いいたします。
