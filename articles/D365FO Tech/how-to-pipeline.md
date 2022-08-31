---
title: Azure PipelinesとMicrosoft-hosted agentsを使用したビルドの手順
date: 2022-08-31
tags:
  - D365FO
  - Azure Pipeline
  - Microsoft-hosted agents
  - Azure DevOps

disableDisclaimer: false
---

こんにちは、日本マイクロソフトの佐藤です。

この記事では、Azure PipelinesとMicrosoft-hosted agentsを使用したビルドの手順をまとめます。AzureDevOpsとVMのリモートデスクトップ画面から、この手順を行うことを推奨いたします。

<!-- more -->

本記事は下記の5つの項目から構成されています。

[ステップ1:AzureDevOpsでプロジェクトの作成](#ステップ1:AzureDevOpsでプロジェクトの作成)

[ステップ2:AzureDevOpsのFeedの作成](#ステップ2:AzureDevOpsのFeedの作成)

[ステップ3:AzurePipelineの設定](#ステップ3:AzurePipelineの設定)

[ステップ4:ReleasePipelineで自動アップロード・資産のデプロイを設定](#ステップ4:ReleasePipelineで自動アップロード・資産のデプロイを設定)

[ReleasePipelineで起こる可能性のあるエラー](#ReleasePipelineで起こる可能性のあるエラー)

## ステップ1:AzureDevOpsでプロジェクトの作成
1. Organizationを作成します。
2. New Projectからプロジェクトを作成します。
    <img src="./CreateProject1.png" style="border: 1px black solid;">
    
3. [Repos]で下記のようにフォルダ構成を作成します。
[Trunk] > [Main] > [Metadata]との構成ができていれば大丈夫です。
    <img src="./CreateProject2.png" style="border: 1px black solid;">

4. Visual Studioを開き、Team ExplorerからDevOpsとVMのプロジェクトとソリューション、モデルを同期します。

サンプルとしてModel ManagementからModel1を作成します。名前とPublisher以外の設定は変更しません。
    <img src="./CreateProject3.png" style="border: 1px black solid;">
    <img src="./CreateProject4.png" style="border: 1px black solid;">

Model1を使用して、プロジェクトを作成し、プロジェクト内にサンプルとして下記のコードを用いたクラスを作成します。
```javascript
class RunnableClass1
{
    public static void main(Args _args)
    {
        Info("Hello World!_Motoki");
    }
}
```
クラス名はRunnableClass1としています。
    <img src="./CreateProject5.png" style="border: 1px black solid;">

作成したクラスはTeam ExplorerからAzure DevOpsに接続します。
    <img src="./CreateProject6.png" style="border: 1px black solid;">

Source Control ExplorerからWorkspaceを作成し、AzureDevOpsと連携させます。
この場合下記のようにWorkspaceが作成できれば大丈夫です。
    <img src="./CreateProject7.png" style="border: 1px black solid;">

5. DevOpsの画面に戻り、[Repos]の形としてはこのように配置されていれば大丈夫です。Nuget.configとpackages.configについては後ほど説明いたします。

またプロジェクトの作成とWorkspaceのマッピングに関する詳細は下記の公開資料をご参照ください。

[Azure DevOpsでのプロジェクト作成](https://docs.microsoft.com/ja-jp/azure/devops/organizations/projects/create-project?view=azure-devops&tabs=browser)

[Visual Studio をコンフィギュレーションしてチーム プロジェクトに接続する](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/dev-tools/version-control-metadata-navigation#map-your-azure-devops-project-to-your-local-model-store-and-projects-folder)

## ステップ2:AzureDevOpsのFeedの作成

以下の手順は、下記のdocsに記載されている手順となっております。

[Microsoft ホステッド エージェントと Azure Pipelines を使用するビルドの自動化](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/dev-tools/hosted-build-automation)

1. まずVMで下記のファイルをまとめるようなフォルダを作成します。ここではフォルダ名をNugetsとします。
    |![](./how-to-pipeline/CreateFeed1.png)|
    |:-:|

    ダウンロードするファイル・フォルダ
    * nuget.exe
    * ~.nupkg
    * netcore
    * netfx

    自分で作成するファイル
    * installcredprovider.ps1
    * ~.config

    これらのファイル、フォルダに関しては後ほど手順を記載します。

2. 次にDevOpsの[Artifacts]から[Feed]の作成を行います。名前以外、設定の変更は特にしません（今回のFeed名は"D365FOAutoBuild"とします）。
    |![](./how-to-pipeline/CreateFeed2.png)|
    |:-:|

3. 作成した[Feed]で、[Connect to Feed] > [Nuget.exe] > [Project setup]の内容をそのままコピーし、nuget.configをVMフォルダ（Nugets）に作成します。
    |![](./how-to-pipeline/CreateFeed3.png)|
    |:-:|
    |![](./how-to-pipeline/CreateFeed4.png)|
    Nuget.config
    |![](./how-to-pipeline/CreateFeed5.png)|
    
4. VMフォルダ（Nugets）に下記のリンクからnuget.exeをダウンロードします。
    https://www.nuget.org/downloads
    |![](./how-to-pipeline/CreateFeed6.png)|
    |:-:|

5. 	下記のgithubからinstallcredprovider.ps1を作成し、ローカルのPowershellで実行します。スクリプトが資格情報を要求し続けて失敗する場合は、パラメーターとして -AddNetfx を追加してみてください。

	https://github.com/Microsoft/artifacts-credprovider/blob/master/helpers/installcredprovider.ps1

    |![](./how-to-pipeline/CreateFeed1-2.png)|
    |:-:|

実行したらpluginのnetcore, netfxのフォルダが作成されるので、Nugetsフォルダにコピーします。

6. LCSプロジェクトの[資産ライブラリ] > [NuGet packages] > [インポート]でデプロイ先のバージョンの.nupkgファイルを4種類ダウンロードします。また、このときの[追加の詳細]の[説明]からそれぞれのVersionを記録しておきます。
    |![](./how-to-pipeline/CreateFeed7.png)|
    |:-:|
    |![](./how-to-pipeline/CreateFeed8.png)|
    
ダウンロードした.nupkgファイルのVersionに沿ってPackages.configを作成します。下記のコードのVersionは.nupkgファイルの情報によって随時変更してください。
|![](./how-to-pipeline/CreateFeed9.png)|
|:-:|

```javascript
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="Microsoft.Dynamics.AX.Platform.DevALM.BuildXpp" version="7.0.6395.47" targetFramework="net40" />
    <package id="Microsoft.Dynamics.AX.Application.DevALM.BuildXpp" version="10.0.1227.52" targetFramework="net40" />
    <package id="Microsoft.Dynamics.AX.ApplicationSuite.DevALM.BuildXpp" version="10.0.1227.52" targetFramework="net40" />
    <package id="Microsoft.Dynamics.AX.Platform.CompilerPackage" version="7.0.6395.47" targetFramework="net40" />
</packages>
```
7. PowershellからAzure DevOpsのFeedに.nupkgファイルを送ります。
※このときにリモートデスクトップ画面から行うと通信速度が早い可能性があります。
    |![](./how-to-pipeline/CreateFeed10.png)|
    |:-:|

```javascript
	.\nuget.exe push -Source "対象のFeed名" -ApiKey az Microsoft.Dynamics.AX.Application.DevALM.BuildXpp.nupkg -Timeout 3600
	.\nuget.exe push -Source "対象のFeed名" -ApiKey az Microsoft.Dynamics.AX.Platform.DevALM.BuildXpp.nupkg -Timeout 3600
	.\nuget.exe push -Source "対象のFeed名" -ApiKey az Microsoft.Dynamics.AX.Platform.CompilerPackage.nupkg -Timeout 3600
    .\nuget.exe push -Source "対象のFeed名" -ApiKey az Microsoft.Dynamics.AX.ApplicationSuite.DevALM.BuildXpp.nupkg -Timeout 3600
```

UserNameとパスワードを求められます
* UserNameはAzureDevOpsのサインインアカウント
* PasswordはPersonal Access Tokenで作成
|![](./how-to-pipeline/CreateFeed13.png)|
|:-:|

## ステップ3:AzurePipelineの設定
1. 	下記から、定義済みのパイプラインのダウンロードを行います（xpp-classic-ci.json）
https://github.com/microsoft/Dynamics365-Xpp-Samples-Tools/tree/master/CI-CD/Pipeline-Samples
    |![](./how-to-pipeline/CreatePipe1.png)|
    |:-:|

2. Pipelineを作成します。
    |![](./how-to-pipeline/CreatePipe2.png)|
    |:-:|
3. 先ほどダウンロードしたxpp-classic-ci.jsonを[Import a pipeline]で選択します。
    |![](./how-to-pipeline/CreatePipe3.png)|
    |:-:|
    
4. Pipelineは下記のようになります。
    |![](./how-to-pipeline/CreatePipe4-0.png)|
    |:-:|
タスクIDの不一致により、テンプレート内の古いタスクが認識されないと思われます。そのため、古いタスクを削除し、同じ新しいタスクを1つ追加してください。以下のスクリーンショットが今回作成するパイプラインになります。
|![](./how-to-pipeline/CreatePipe4.png)|
|:-:|

該当のタスクが見つからない場合、下記のDynamics 365 Finance and Operations Toolsのインストールを確認してください。
https://marketplace.visualstudio.com/items?itemName=Dyn365FinOps.dynamics365-finops-tools

|![](./how-to-pipeline/CreatePipe4-1.png)|
|:-:|

5. 各タスクを設定していきます。
* Pipeline

|![](./how-to-pipeline/CreatePipe5.png)|
|:-:|

* Get sources

|![](./how-to-pipeline/CreatePipe7.png)|
|:-:|

* Nuget installer

|![](./how-to-pipeline/CreatePipe8.png)|
|:-:|

* Update Model Version

|![](./how-to-pipeline/CreatePipe9.png)|
|:-:|

* Visual Studio Build
MSBuild Argumentsには下記を入力します
```javascript
/p:BuildTasksDirectory="$(NugetsPath)\$(ToolsPackage)\DevAlm"  /p:MetadataDirectory="$(MetadataPath)"  /p:FrameworkDirectory="$(NuGetsPath)\$(ToolsPackage)"  /p:ReferenceFolder="$(NuGetsPath)\$(PlatPackage)\ref\net40;$(NuGetsPath)\$(AppPackage)\ref\net40;$(NuGetsPath)\$(AppSuitePackage)\ref\net40;$(MetadataPath);$(Build.BinariesDirectory)"  /p:ReferencePath="$(NuGetsPath)\$(ToolsPackage)"  /p:OutputDirectory="$(Build.BinariesDirectory)"
```
その他はスクリーンショットをご参照ください

|![](./how-to-pipeline/CreatePipe10.png)|
|:-:|

* Copy Files

|![](./how-to-pipeline/CreatePipe11.png)|
|:-:|

* NuGet Tool Installer

|![](./how-to-pipeline/CreatePipe12.png)|
|:-:|

* Create Deployable Package

|![](./how-to-pipeline/CreatePipe13-1.png)|
|:-:|

* Publish Artifact: drop

|![](./how-to-pipeline/CreatePipe14.png)|
|:-:|

6. [Save & Queue]を実行します。Artifactができれば成功です。

|![](./how-to-pipeline/CreatePipe15.png)|
|:-:|

## ステップ4:ReleasePipelineで自動アップロード・資産のデプロイを設定

2022/08/29の時点で、LCS 認証には、多要素認証(MFA) が有効になっていない AAD アカウントが必要です。現在、LCSの新しい認証機能として、サービス間認証などのオプションを検討中です。また以下の手順は、下記のdocsに記載されている手順となっております。

[Azure Pipelines で LCS 接続を作成する](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/dev-tools/pipeline-lcs-connection)

[Azure Pipelines を使用した資産のアップロード](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/dev-tools/pipeline-asset-upload)

[Azure Pipelines を使用した資産のデプロイ](https://docs.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/dev-tools/pipeline-deploy-asset)

1. Azure Active Directory アプリケーションを作成します

    1. Azure ポータル(https://ms.portal.azure.com/#home) > Azure Active Directory > 管理 > アプリの登録に移動します。
	2. [新規登録] をクリックし、名前を入力して [登録]をクリックします。
	3. アプリケーションの詳細画面から、[管理] > [API のアクセス許可] > [構成されたアクセス許可] > [アクセス許可の追加] に移動します
	4. [所属する組織で使用している API] の下の[ Dynamics Lifecycle services] を選択します。
	5. [user_impersonation]権限を追加します
	6. [Microsoftに管理者の同意を与えます]をクリックします
	
	|![](./how-to-pipeline/CreateDeploy1.png)|
	|:-:|

   7. アプリケーションの詳細画面の[管理] > [認証] に移動します
   8. [詳細設定] > [パブリック クライアント フローを許可する] で、[次のモバイルおよびデスクトップ フローを有効にする]を [はい]に構成します。
   
   |![](./how-to-pipeline/CreateDeploy2.png)|
   |:-:|

2. Azure DevOps でLCSへのサービス接続を作成します

    1. DevOps プロジェクトの [プロジェクト設定] > [パイプライン] > [サービス接続] に移動します。
    2. [新しいサービス接続]をクリックします
    
    |![](./how-to-pipeline/CreateDeploy3.png)|
    |:-:|

    3. [Dynamics Lifecycle Services]を選択します
    4. 次の詳細を入力します。
        ユーザー名:プロジェクトとアセット ライブラリにアクセスできる LCS 資格情報
        パスワード:ユーザー名で使用したアカウントのパスワード
        アプリケーション ID:これは、前のステップで作成されたアプリケーションのアプリ/クライアント ID です。
        サービス接続名:任意の名前を指定します

        下記のスクリーンショットの黄色の四角には同じドメインを入力してください。
	
    |![](./how-to-pipeline/CreateDeploy4.png)|
    |:-:|
    
    5. [保存]をクリック

3. リリースパイプラインを作成します
    1. [Pipeline] > [Releases] > [New] > [New Release pipeline]を開きます。（名前を"Upload and Deploy"としています）
    
    |![](./how-to-pipeline/CreateDeploy5.png)|
    |:-:|

    2. [Artifact] > [Add]から作成したPipelineを選択します。また、[Stages] > [Add] > [New Stage]からStageを作成します。
    
    |![](./how-to-pipeline/CreateDeploy6.png)|
    |:-:|

    3. [Task]バーからtaskを作成します。
* Agent jpb

|![](./how-to-pipeline/CreateDeploy7.png)|
|:-:|
	
* Insatll MSAL.PS to enable authentication
	
|![](./how-to-pipeline/CreateDeploy8.png)|
|:-:|
	
* Dynamics Lifecycle Servicies (LCS) Asset Upload

LCS Project IDは、デプロイ対象の環境をブラウザで開いた際のURLの末尾にある数字7桁を入力します
	
|![](./how-to-pipeline/CreateDeploy10.png)|
|:-:|
|![](./how-to-pipeline/CreateDeploy9.png)|
	
* Dynamics Lifecycle Servicies (LCS) Asset Deployment
        
|![](./how-to-pipeline/CreateDeploy11.png)|
|:-:|
	
4. Artifactの右上のマークから[Continuous deployment trigger]を[Enabled]に設定して、[Create release]をすると、Pipelineのビルドが終わったときに自動的にリリースパイプラインが実行されます。

|![](./how-to-pipeline/CreateDeploy12.png)|
|:-:|

## ReleasePipelineで起こる可能性のあるエラー
* 環境の不一致では下記のエラーが確認されます

|![](./how-to-pipeline/CreateDeploy13.png)|
|:-:|

```javascript
##[error]Error in request to deploy file asset: 'Deployable package environment validation failed' (Operation Activity Id: '~~~~~~~~~~~~~~~~~~~')
```
.nupkgの対象のバージョンと、デプロイ先の環境のバージョンが一致することを確かめてください。

* LCSへの接続で下記のようなエラーが発生することがあります。
```javascript
##[error]The process '/usr/bin/docker' failed with exit code 1
```
その際は[Feed] > [Feed Setting] > [Add users/group]で『"プロジェクト名"（組織名）』で"Contributor"を選択すると解決する可能性がございます。

|![](./how-to-pipeline/CreateDeploy14.png)|
|:-:|


## 注意
上記の手順、手順内の画像については本記事の執筆時のものです。
実際の画面とは挙動に違いがある可能性がございます。

---
## おわりに  

以上、Dynamics 365 Finance and Operationsにて、LCSからWinRM証明書のエラーが出た際の対処法をご紹介させていただきました。
もし、お困りのこと等がございましたら、弊社までお問い合わせ頂きますようお願いいたします。
