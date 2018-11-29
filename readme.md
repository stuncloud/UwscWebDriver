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

### Edge

1. 管理者として実行したコマンドプロンプト、またはPowerShellから以下を実行する

    ```
    DISM.exe /Online /Add-Capability /CapabilityName:Microsoft.WebDriver~~~~0.0.1.0
    ```

### Chrome

1. [ここ](https://sites.google.com/a/chromium.org/chromedriver/downloads)から `Latest Release` のリンクを開いて `chromedriver_win32.zip` をダウンロード
2. zipの中の `chromedriver.exe` を実行するスクリプトと同じフォルダに置く

### Firefox

1. [ここ](https://github.com/mozilla/geckodriver/releases)から `geckodriver-vX.XX.X-winXX.zip` をダウンロード
2. zipの中の `geckodriver.exe` を実行するスクリプトと同じフォルダに置く

※ 32か64は環境に合わせてください

### その他のWebDriver

WebDriverのexeを実行するスクリプトと同じフォルダに置いてください

jsonパーサ
----------

json処理のために `json2.js` を使います  
[ここ](https://github.com/douglascrockford/JSON-js)からダウンロードして実行するスクリプトと同じフォルダに置いてください

使い方
------

### 準備

- 使用するWebDriverを実行するスクリプトと同じフォルダに置く
- `json2.js` を実行するスクリプトと同じフォルダに置く
- `UwscWebDriver.uws` を実行するスクリプトと同じフォルダに置く
- 実行するスクリプトで `UwscWebDriver.uws` を `call` する

### リファレンスガイド

https://stuncloud.github.io/UwscWebDriver/


サンプルスクリプト
------------------

- sample.uws  
    [日本Seleniumユーザーコミュニティにあるテスト用サイト](http://www.selenium.jp/test-site) を使ったサンプルです

