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

##### WebDriver.CreateJSArray()

JavaScriptの配列を得ます  
`push()` で要素を追加できます

- 戻り値  
    空のJavaScript配列

```
arr = WebDriver.CreateJSArray()
arr.push("hoge")
arr.push("fuga")
arr.push("piyo")
```

##### WebDriver.GetError()

`webdriverオブジェクト` や`webelementオブジェクト` 起因のCOMエラーが発生した際のエラー詳細を得ます

- 戻り値  
    エラー詳細(文字列)


### webdriverオブジェクト

WebDriver.Start() が返すオブジェクトです  

#### メソッド

##### Navigate(url[, target])

- url  
    指定したURLを開きます
- target  
    省略可  
    値を指定した場合は別タブで開かれます
- 戻り値  
    なし

```
// 任意のURLを開く
driver.Navigate(url)
// 任意のURLを別タブで開く
driver.Navigate(url, "_blank")
```

##### SwitchWindow(handleOrName)

別のウィンドウ(タブ)に制御を移します

- handleOrName  
    ウィンドウハンドル、またはウィンドウ名  
    ウィンドウ名は `window.name` です  
    targetで別名指定されていた場合などに使います  
    ただしハンドルを指定するより遅いです
- 戻り値  
    制御を移したウィンドウのハンドル

```
// 元のタブのウィンドウハンドルを得る
hFirst = driver.GetCurrentWindowHandle()
// 別タブを開く
driver.Navigate(url, "SecondTab")
// 別タブに制御を移す
hSecond = driver.SwitchWindow("SecondTab")
// 元のウィンドウに戻る
driver.SwitchWindow(hFirst)
```

##### GetCurrentWindowHandle()

現在の制御対象ウィンドウのハンドルを得ます

- 戻り値  
    ウィンドウハンドル

##### GetWindowHandles()

制御可能なウィンドウのハンドルを列挙します

- 戻り値  
    ウィンドウハンドルの配列(SafeArray)

```
for h in driver.GetWindowHandles()
    driver.SwitchWindow(h)

    // それぞれのウィンドウに対する処理を実行
    DoSomoThing(driver)
next
```

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

##### ExecuteScript(script[, args])

任意のJavaScriptを実行させます

- script  
    JavaScriptのスクリプト構文  
- args  
    JavaScript配列 (省略可)  
    実行するスクリプトに渡したい値を指定します
    `script` 内で `arguments[]` としてこの値にアクセスできます
- 戻り値  
    `script` 内で `return` した値

```
elem = driver.FindElement(selector)

textblock js
arguments[0].style.backgroungColor = arguments[1];
return arguments[0].outerHTML;
endtextblock

// js配列を作る
args = WebDriver.CreateJSArray()
// js要素を足す
// elementオブジェクトも渡せる、その場合raw()メソッドを使う
args.push(elem.raw())
// 文字列とかでも当然OK
args.push("red")

driver.ExecuteScript(js, args)
```

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

##### raw()

WebDriverが返す元々のJavaScriptオブジェクトを得る  
`ExecuteScript()` の `args` に渡す場合に使う

- 戻り値  
    jsオブジェクト
