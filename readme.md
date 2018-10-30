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

1. `MicrosoftWebDriver.exe` を[ここ](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/#downloads)からダウンロード
2. `MicrosoftWebDriver.exe` を実行するスクリプトと同じフォルダに置く

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

### 関数

#### WebDriver.Start(driverpath[, port])

WebDriverを起動して、セッションIDを取得します  
(コマンドプロンプトの画面が表示されます)

- driverpath  
    Chromeなら `WebDriver.Chrome`  
    MS Edgeなら `WebDriver.Edge`  
    Firefoxなら `WebDriver.Firefox`  
    を指定します  
    それ以外のWebDriverの場合はexeのフルパスを指定してください
- port  
    省略可能  
    WebDriverの待受ポート番号を指定します  
    デフォルトは `9515` です
- 戻り値
    - 成功時  
        sessionId
    - 失敗時  
        EMPTY

#### WebDriver.Navigate(sessionId, uri)

指定したURLを開きます

- sessionId  
    `WebDriver.Start` の戻り値
- uri  
    開きたいURL
- 戻り値  
    なし

#### WebDriver.GetURL(sessionId)

現在開いているページのURLを取得します

- sessionId  
    `WebDriver.Start` の戻り値
- 戻り値  
    URL

#### WebDriver.FindElement(sessionId, selector)

cssセレクタを指定して対象エレメントのIDを取得します

- sessionId  
    `WebDriver.Start` の戻り値
- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    elementId

#### WebDriver.FindElements(sessionId, selector)

cssセレクタを指定して対象エレメントのIDを配列で取得します

- sessionId  
    `WebDriver.Start` の戻り値
- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    elementIdの配列(safearray)

#### WebDriver.SetValue(sessionId, elementId, text)

input[type="text"]等に値を入力します

- sessionId  
    `WebDriver.Start` の戻り値
- text  
    入力する値
- 戻り値  
    なし

#### WebDriver.GetValue(sessionId, elementId)

inputやselect等のvalueの値を取得します

- sessionId  
    `WebDriver.Start` の戻り値
- elementId  
    `WebDriver.FindElement` の戻り値
- 戻り値  
    取得した値


#### WebDriver.Click(sessionId, elementId)

エレメントをクリックします

- sessionId  
    `WebDriver.Start` の戻り値
- elementId  
    `WebDriver.FindElement` の戻り値
- 戻り値  
    なし

#### WebDriver.GetText(sessionId, elementId)

エレメント配下のテキストノードの値を取得します

- sessionId  
    `WebDriver.Start` の戻り値
- elementId  
    `WebDriver.FindElement` の戻り値
- 戻り値  
    取得した値


#### WebDriver.GetAttribute(sessionId, elementId, attribute)

エレメントの属性の値を取得します

- sessionId  
    `WebDriver.Start` の戻り値
- elementId  
    `WebDriver.FindElement` の戻り値
- attribute  
    属性の名前
- 戻り値  
    取得した値

#### WebDriver.Close(sessionId)

セッションを終了しブラウザを閉じます  
WebDriverは起動したままなので、WebDriverを終了させたい場合は手動でコマンドプロンプトを閉じてください

- sessionId  
    `WebDriver.Start` の戻り値
- 戻り値  
    なし


