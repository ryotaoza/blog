---
title: 請求後の発注書の編集制御方法
date: 2022-5-24
tags: 
    - D365FO
    - Purchase order
    - Procurement and sourcing parameters
    
disableDisclaimer: false
---

こんにちは、Dynamics ERP サポートの木村です。  
この記事では、請求後の発注書の編集を制御するパラメータについてご案内いたします。  

<!-- more -->
## 検証に用いた製品・バージョン
Dynamics 365 Finance and Operations      
Application version: 10.0.24  
Platform version: PU48

パラメータの適用方法、動作につきましては以下をご覧ください。  

## 請求後の発注書の編集制御方法
### 「請求済注文の安全レベル」を**警告**に変更した場合
1. 調達 > 設定 > 調達パラメーターを開く
1. 配送日タブを開く
1. 「請求済注文の安全レベル」を**ロック済**に変更し、保存する
![](./restrict-po-edit/restrict-po-edit_1.png)
1. 請求済の発注書を開く  </br></br>
**-> 明細行の追加などのボタンが非活性になる**
![](./restrict-po-edit/restrict-po-edit_2.png)
***  

### 「請求済注文の安全レベル」を**警告**に変更した場合
![](./restrict-po-edit/restrict-po-edit_3.png)
1. 明細行の追加などのボタンを押下する
1. 以下ダイアログが表示され、「はい」を押下する  
![](./restrict-po-edit/restrict-po-edit_4.png)   </br></br>
**-> ダイアログは表示されるが、請求済の発注書は編集可能となる**
![](./restrict-po-edit/restrict-po-edit_5.png)
***  

### 「請求済注文の安全レベル」を**なし**に変更した場合
![](./restrict-po-edit/restrict-po-edit_6.png)</br></br>
**-> 請求済の発注書は常に編集可能**

## おわりに
---
以上、請求後の発注書の編集を制御するパラメータについてご紹介いたしました。  
請求した発注書に対して編集を制御されたいなどの場合には、上記パラメータをご利用ください。
