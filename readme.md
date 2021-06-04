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
※ 旧Edgeのdriverはスクリプト実行フォルダではなくシステムフォルダに配置されます

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

使い方
------

### 準備

- 使用するWebDriverを実行するスクリプトと同じフォルダに置く  
    ※ PATHの通してあるフォルダにWebDriverが置いてある場合は不要
- `UwscWebDriver.uws` を実行するスクリプトと同じフォルダに置く
- 実行するスクリプトで `UwscWebDriver.uws` を `call` する

### モジュールの詳細

[[UWSCWebDriver Wiki|Home#使い方]]

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

### 不具合報告フォーマット

掲示板ではなるべく以下のフォーマットに沿って質問してください

```markdown
# 質問

質問したい内容を完結に記述してください

# 目的

最終的にどのような成果を得たいかをなるべく具体的に記述してください  
質問箇所だけではなく、やりたい一連の作業について書いてください  

# 操作手順

目的を達成するためにどのような操作を行うかの手順を記述してください  
手で操作する場合はこのようにやる、といった情報で構いません  
そのうちどこがわからず詰まっているか(質問箇所)も書いておいてください

1. 〇〇をクリック
2. 表示された〇〇から□□を探しクリックする ←ここがわからない
3. 表示された○○に□□を入力する
4. ○○ボタンを押し入力を確定する
5. 上記を○○ごとに繰り返し行う

# 操作対象の情報

- 利用したブラウザ
- 対象サイトのURL
    - ログインが必要かどうかなど

# 実行したコード

目的のために記述したコード  
※ あまり長くなりすぎないように該当箇所だけ書くなどの工夫をお願いします

# うまく行かない点

実行したコードがどのようにうまく行かなかったのかの説明

```