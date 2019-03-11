{:toc}

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
    - 失敗時  
        null

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
    - 成功時  
        webelementオブジェクト
    - 失敗時  
        null

##### FindElements(selector)

cssセレクタを指定して該当する複数のエレメントの `webelementオブジェクト` を取得します

- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    - 成功時  
        webelementオブジェクト配列 (SafeArray)
    - 失敗時  
        null

##### FindElementsByName(name)

name属性の値を指定して該当する複数のエレメントの `webelementオブジェクト` を取得します

- selector  
    対象エレメントのname属性
- 戻り値  
    - 成功時  
        webelementオブジェクト配列 (SafeArray)
    - 失敗時  
        null

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
    - 成功時  
        webelementオブジェクト
    - 失敗時  
        null

##### FindElements(selector)

対象エレメントを起点としたcssセレクタを指定して該当する複数のエレメントの `webelementオブジェクト` を取得します

- selector  
    対象エレメントのcssセレクタ
- 戻り値  
    - 成功時  
        webelementオブジェクト配列 (SafeArray)
    - 失敗時  
        null

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
