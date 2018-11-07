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

### WebDriverモジュール

#### 関数

##### WebDriver.Start(driverpath[, port])

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
        webdriverオブジェクト

##### WebDriver.GetError()

`webdriverオブジェクト` や`webelementオブジェクト` 起因のCOMエラーが発生した際のエラー詳細を得ます

- 戻り値  
    エラー詳細(文字列)


### webdriverオブジェクト

WebDriver.Start() が返すオブジェクトです  

#### メソッド

##### Navigate(url)

- url  
    指定したURLを開きます
- 戻り値  
    なし

##### GetUrl()

現在開いているページのURLを取得します

- 戻り値  
    URL

##### FindElement(selector)

cssセレクタを指定して該当するエレメントの `webelementオブジェクト` を取得します

- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    webelementオブジェクト

##### FindElements(selector)

cssセレクタを指定して該当する複数のエレメントの `webelementオブジェクト` を取得します

- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    webelementオブジェクト配列 (SafeArray)

##### Close()

セッションを終了しブラウザを閉じます  
WebDriverは起動したままなので、WebDriverを終了させたい場合は手動でコマンドプロンプトを閉じてください

- 戻り値  
    なし

### webelementオブジェクト

`webdriverオブジェクト` や`webelementオブジェクト` の `FindElement()` および`FindElements()` が返すオブジェクトです

#### メソッド

##### FindElement(selector)

対象エレメントを起点としたcssセレクタを指定して該当するエレメントの `webelementオブジェクト` を取得します

- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    webelementオブジェクト

##### FindElements(selector)

対象エレメントを起点としたcssセレクタを指定して該当する複数のエレメントの `webelementオブジェクト` を取得します

- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    webelementオブジェクト配列 (SafeArray)

##### Click()

エレメントをクリックします

- 戻り値  
    なし

##### SetValue(value)

input[type="text"]等に値を入力します

- value  
    入力する値
- 戻り値  
    なし

##### GetValue()

inputやselect等のvalueの値を取得します

- 戻り値  
    取得した値

##### GetText()

エレメント配下のテキストノードの値を取得します

- 戻り値  
    取得した値

##### GetAttribute(attribute)

エレメントの属性の値を取得します

- attribute  
    属性の名前
- 戻り値  
    取得した値

##### IsSelected()

ラジオボタン等が選択されているかどうかを取得します

- 戻り値  
    bool値
