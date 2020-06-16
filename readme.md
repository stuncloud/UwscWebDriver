UwscWebDriver
=============

WebDriverとのやり取りを行うためのUWSCモジュールです  
WebDriverさえあればブラウザの自動化が可能になります  
(つまりSelenium等が不要になります…が機能面では劣る)

WebDriverについて
-------------

[仕様](https://w3c.github.io/webdriver/)

WebDriver導入方法
-------------

### ダウンロード用スクリプトを実行する

`UwscWebDriver.uws`に含まれるWebDriverDownloadモジュールによって各種WebDriverの導入および更新が可能です

#### GUIから導入するWebDriverを選ぶ

Edge(新旧)、Chrome、Firefoxに対応

```
call UwscWebDriver.uws

WebDriverDownload.Dialog()
```

#### 個別に導入する

```
call UwscWebDriver.uws

// MicrosoftWebDriverを有効にする
// UACの昇格ダイアログが表示されます
WebDriverDownload.EdgeLegacy()

// msedgedriverをダウンロードする
// Chromium Edgeのメジャーバージョンが83の場合、引数に83を渡す
WebDriverDownload.ChromiumEdge(83)

// chromedriverをダウンロードする
// Google Chromeのメジャーバージョンが75の場合、引数に75を渡す
WebDriverDownload.Chrome(75)

// 最新のgeckodriverをダウンロードする
// 引数に32を渡すと32bit版、64を渡すと64bit版がダウンロードされます
WebDriverDownload.Firefox(64)

```

### 手動で導入する

#### Edge

1. 管理者として実行したコマンドプロンプト、またはPowerShellから以下を実行する

    ```
    DISM.exe /Online /Add-Capability /CapabilityName:Microsoft.WebDriver~~~~0.0.1.0
    ```

#### Chrome

> Google Chrome と chromedriver のバージョンは必ず合わせてください  
> 特にメジャーバージョンがずれると予期せぬ不具合が生じる可能性があります

1. [ここ](https://sites.google.com/a/chromium.org/chromedriver/downloads)から `Latest Release` のリンクを開いて `chromedriver_win32.zip` をダウンロード
2. zipの中の `chromedriver.exe` を実行するスクリプトと同じフォルダに置く

#### Firefox

1. [ここ](https://github.com/mozilla/geckodriver/releases)から `geckodriver-vX.XX.X-winXX.zip` をダウンロード
2. zipの中の `geckodriver.exe` を実行するスクリプトと同じフォルダに置く

※ 32か64かは環境に合わせてください

#### Chromium Edge

> Chromium Edge と msedgedriver のメジャーバージョンは必ず合わせてください  
> バージョンが異なると動作しません

1. [ここ](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/#downloads)からMicrosoft Edgeの任意のバージョンのリンク(x86かx64)をクリックし、`edgedriver_winXX.zip` をダウンロード  
    ※ Legacyは旧版なのでダウンロードしないでください  
2. zipの中の `msedgedriver.exe` を実行するスクリプトと同じフォルダに置く

#### その他のWebDriver

WebDriverのexeを実行するスクリプトと同じフォルダに置いてください

### PackageManagementによるWebDriverの導入

PowerShellのパッケージ管理を利用したインストール方法です  
Windows10では標準で使えます  
8.1や7は別途PackageManagementを導入する必要があります

以下はすべて「管理者として実行」したPowerShellで実行してください

#### Chocolatierの導入方法

Chocolatierがインストールされていない場合は以下を実行します

```PowerShell
Install-PackageProvider -Name Chocolatier
Import-PackageProvider -Name Chocolatier
```

#### WebDriverのインストール

- 途中何度かpromptが表示されるので`y`を入力してください
- `-Force`スイッチを付与することでpromptを省略できます

PATHの通ったディレクトリに置かれるはずなのでこの方法でインストールすれば使えるようになります

##### Chrome

```PowerShell
Install-Package -Provider Chocolatier -Name chromedriver
```

##### Firefox

```PowerShell
Install-Package -Provider ChocolateyGet -Name selenium-gecko-driver
```

##### Chromium Edge

```PowerShell
Install-Package -Provider ChocolateyGet -Name selenium-chromium-edge-driver
```

使い方
------

### 準備

- 使用するWebDriverを実行するスクリプトと同じフォルダに置く  
    ※ PATHの通してあるフォルダにWebDriverが置いてある場合は不要
- `UwscWebDriver.uws` を実行するスクリプトと同じフォルダに置く
- 実行するスクリプトで `UwscWebDriver.uws` を `call` する

### リファレンスガイド

https://stuncloud.github.io/UwscWebDriver/


サンプルスクリプト
------------------

[日本Seleniumユーザーコミュニティにあるテスト用サイト](http://www.selenium.jp/test-site) を使ったサンプルです

- sample.uws
    - [その1](http://example.selenium.jp/reserveApp/)
- sample2.uws
    - [その2](http://example.selenium.jp/reserveApp_Renewal/)

質問や不具合の報告など
----------------------

[こちら](https://github.com/stuncloud/UwscWebDriver/issues) でお願いします  
[UWSC仮掲示板](http://www3.rocketbbs.com/601/siromasa.html) でも気付けば反応します
