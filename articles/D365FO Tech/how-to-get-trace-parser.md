---
title: Trace Parserを使用したトレースの実行方法
date: 2022-09-29
tags:
  - D365FO
  - trace parser
  - tips

disableDisclaimer: false
---

こんにちは、日本マイクロソフト Dynamics ERP サポートチームの道浦です。  
この記事では、 Dynamics 365 Finance and Operations にて、 Trace Parser を使用したトレースの実行手順を紹介します。

<!-- more -->
## 検証に用いた製品・バージョン
Dynamics 365 Finance and Operations      
Application version: 10.0.29  
Platform version: PU53  



## Trace Parser を使用したトレースの実行手順

* **Admin 権限を持っているユーザー**

1. ヘッダー部分の「?」から「追跡」を選択する

    ![](./how-to-get-trace-parser/step.png)


2. 追跡名に任意の名称を入力し、「追跡の開始」をクリックする
     ![](./how-to-get-trace-parser/step2.png)


3. 任意の操作を行い、トレースの実行を終了する際は、「追跡の停止」をクリックする
     ![](./how-to-get-trace-parser/step3.png)


4.  実行したトレースをローカルマシーンに保存する場合は、「トレースのダウンロード」をクリックする
     ![](./how-to-get-trace-parser/step4.png)

 * **Admin 権限を持っていないユーザー(システムトレースユーザー権限付与済)**

5. 手順 3 まで同様に進める


6. トレースの取得が完了したら「トレースのアップロード」をクリックする  
トレースのアップロードが完了すると、admin 権限のあるユーザーに送信される

     ![](./how-to-get-trace-parser/step6.png)


## アップロードされたトレースの確認手順

7. 手順 1 と同様に進め、「追跡」のメニューから「キャプチャされたトレース」をクリックする

     ![](./how-to-get-trace-parser/step7.png)
    
8. 対象の追跡名をクリックし、ダウンロードする  
ここで、権限を持たないユーザーがアップロードしたトレースを確認することができます。

     ![](./how-to-get-trace-parser/step8.png)



## 参考
Trace Parserを使用したトレースの実行方法は、公式ドキュメントでも公開されています。  
下記のリンクも併せてご参照ください。  
https://learn.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/perf-test/trace-trace-tutorial


---
## おわりに  

以上、 Dynamics 365 Finance and Operations にて、 Trace Parser を使用したトレースの実行手順についてご紹介しました。
より詳細な情報が必要な場合、弊社テクニカルサポート, Customer Success Account Manager (CSAM), Customer Engineer (CE) までお問い合わせください。
