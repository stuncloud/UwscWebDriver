{:toc}

### WebDriverモジュール

#### 関数

##### WebDriver.Version()

モジュールのバージョンを得ます

- 戻り値  
    モジュールのバージョン

##### WebDriver.HideCmd()

`WebDriver.Start()` 実行時にコマンドプロンプトの画面表示されなくなります  
(`WebDriver.Start()` の前に呼ぶ必要があります)  
スクリプト終了後もコマンドプロンプトは非表示のまま残ります  
不要な場合はタスクマネージャ等で終了させてください

##### WebDriver.Start(driverpath[, port[, capabilities]])

WebDriverとブラウザを起動してwebdriverオブジェクトを取得します  
事前に `WebDriver.HideCmd()` を実行していない場合、コマンドプロンプトの画面が表示されます

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

##### WebDriver.Remote(remotehost, port, capabilities)

`selenium-server-standalone.jar`を実行しているPC上のWebDriverに接続します

- remotehost  
    リモートPCのホスト名またはIPアドレス  
    ローカルで`selenium-server-standalone.jar`を実行している場合は`localhost`
- port  
    Selenium standalone serverの待ち受けポートです  
    デフォルトは`4444`のようです
- capabilities  
    capabilitiesのjson文字列  
    以下の定数が定義されています  
    Edge: `WebDriver.RemoteEdgeCapabilities`  
    Chrome: `WebDriver.RemoteChromeCapabilities`  
- 戻り値
    - 成功時  
        webdriverオブジェクト
    - 失敗時  
        null

```
remotedriver = WebDriver.Remote("192.168.x.x", "4444", WebDriver.RemoteChromeCapabilities)
```

##### WebDriver.Connect(session)

以前のwebdriverセッションを再利用し、起動済みのブラウザを再び操作できるようにします

- session  
    `webdriver.GetSession()` で取得したセッション情報
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

### WebDriverDownloadモジュール

#### 関数

##### WebDriverDownload.Edge()

Edge用のWebdriverを有効化します

- 戻り値
    - 成功時  
        MicrosoftWebDriverのバージョン
    - 失敗時  
        EMPTY

##### WebDriverDownload.Chrome(major)

chromedriverをダウンロードします

- major
    操作するGoogle Chromeのメジャーバージョン
    例: 75.0.3770.100 であれば 75
- 戻り値
    - 成功時  
        chromedriverのバージョン
    - 失敗時  
        EMPTY

##### WebDriverDownload.Firefox(bit)

geckodriverをダウンロードします

- bit
    `32`または`64`を指定
    操作するFirefoxに合わせる
- 戻り値
    - 成功時  
        geckodriverのバージョン
    - 失敗時  
        EMPTY

##### WebDriverDownload.Dialog()

GUIに従いwebdriverのダウンロード・有効化を行います

- 戻り値
    - 成功時  
        有効化またはダウンロードしたwebdriverのバージョン
    - 失敗時  
        EMPTY

### webdriverオブジェクト

WebDriver.Start() が返すオブジェクトです  

#### メソッド

注意：メソッド名は大文字小文字まで一致している必要があります

#### GetSession()

現在のwebdriverセッション情報を取得します

- 戻り値  
    セッション情報 (文字列)

#### GetBrowserName()

操作対象ブラウザの名前を取得します

- 戻り値  
    ブラウザ名 (文字列)

#### GetBrowserVersion()

操作対象ブラウザのバージョンを取得します

- 戻り値  
    ブラウザバージョン (文字列)

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

##### Reload()

開いているページをリロードします

- 戻り値  
    なし

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

##### GetTitle()

現在開いているページのタイトルを取得します

- 戻り値  
    タイトル

##### GetSource()

現在開いているページのHTMLソースを取得します

- 戻り値  
    HTMLソース

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

##### GetDialogText()

`window.alert()`, `window.confirm()`, `window.prompt()` で表示されたダイアログのテキストを取得します

- 戻り値  
    ダイアログに表示されたテキスト

##### SetDialogText(value)

`window.prompt()` で表示されたプロンプトに値を入力します  
`window.alert()`, `window.confirm()` に対しては無効です

- value  
    ダイアログに入力する値
- 戻り値  
    なし

##### AcceptDialog()

`window.alert()`, `window.confirm()`, `window.prompt()` のOKボタンを押します

- 戻り値  
    なし

##### DismissDialog()

`window.alert()`, `window.confirm()`, `window.prompt()` のキャンセルボタンを押します  
(`window.alert()` にキャンセルボタンはありませんが閉じられます)

- 戻り値  
    なし

##### GetRect()

ブラウザのサイズと座標を取得します

- 戻り値  
    Rectオブジェクト  
    以下のフィールドを持ちます  
    - width (幅)
    - height (高さ)
    - x (x座標)
    - y (y座標)

```
rect = driver.GetRect()
if (rect <> null) then
    with rect
        print "幅: " + .width
        print "高さ: " + .height
        print "x座標: " + .x
        print "y座標: " + .y
    endwith
endif
```

##### SetRect(width, height, x, y)

ブラウザのサイズと座標を変更します

- width  
    ブラウザの幅  
    変更しない場合は`null`にする
- height  
    ブラウザの高さ  
    変更しない場合は`null`にする
- x  
    ブラウザのx座標  
    変更しない場合は`null`にする
- y  
    ブラウザのy座標  
    変更しない場合は`null`にする
- 戻り値  
    Rectオブジェクト  

##### Maximize()

ブラウザを最大化します

- 戻り値  
    Rectオブジェクト  

##### Minimize()

ブラウザを最小化します

- 戻り値  
    Rectオブジェクト  

##### Fullscreen()

ブラウザをフルスクリーン表示します  
※ フルスクリーンに対応しているブラウザのみ

- 戻り値  
    Rectオブジェクト  

##### Close()

セッションを終了しブラウザを閉じます  
WebDriverは起動したままなので、WebDriverを終了させたい場合は手動でコマンドプロンプトを閉じてください

- 戻り値  
    なし

### webelementオブジェクト

`webdriverオブジェクト` や`webelementオブジェクト` の `FindElement()` および`FindElements()` が返すオブジェクトです

#### メソッド

注意：メソッド名は大文字小文字まで一致している必要があります

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
