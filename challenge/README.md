# チャレンジ5

## 目的

- クラスを利用して簡単なアプリを作成する。
- localStorageを利用して、アプリの初期化を行う。
- 外部ライブラリpolyglot.jsを利用する。

## チャレンジの取り組み方

1. スターターファイルのリポジトリを、フォークして自分のGitHubアカウントにリポジトリを作りましょう。
2. マイルストーンごとに要件に合うようにファイルを編集していきます。
3. 分からない部分があれば、テキストを復習して、再度チャレンジしてみましょう。
4. 再チャレンジしてしばらく考えても分からない場合はチャットでメンターに質問しましょう。
5. 完了したら、GitHubリポジトリをメンターにシェアしてください。(質問時に既にシェアしている場合は、レビューを直接依頼しましょう。)
6. メンターから課題レビューが届きます。
7. ビデオチャットの際は、分からない点を更に突っ込んで聞いたり、より良い書き方を聞いてみましょう。

## スターターファイル

- [codegrit-jp-students/js-unit02-ch05-starter](https://github.com/codegrit-jp-students/js-unit02-ch05-starter)

上記のURL先のリポジトリをフォークして、コードを書き進めて行きましょう。

## 概要

Webサービスを展開していくと、英語やスペイン語など複数の言語で同じサービスを提供したいという場面が出てきます。多言語対応のためのライブラリは複数ありますが今回はAirBnBが作成し現在も利用しているライブラリ"polyglot.js"を利用して簡単な多言語アプリを作成します。

[polyglot.jsのドキュメント](http://airbnb.io/polyglot.js/)

## マイルストーン１

polyglot.jsを利用して、日本語のメッセージをpolyglot経由で表示しましょう。

### 要件

1. サイトが立ち上がった時に、TranslationAppクラスをインスタンス化します。
2. polyglot.jsのextendファンクションを利用して"こんにちは、世界"というメッセージを登録します。
3. showMessageファンクションを実装して、メッセージを表示します。


## マイルストーン2

ボタンを押すと現在のlocaleを変更するようにしましょう。localeとはプログラミングにおいて場所や言語の設定のことを指します。今回は`locale="en"`の際は英語のメッセージを表示し、`locale="ja"`の際は日本語のメッセージを表示します。

### 要件

1. インスタンス変数としてcurrentLocaleという値を作成し、デフォルトで"ja"をセットします。
2. updateLocaleファンクションを実装し、ボタンのクリックで現在のlocaleが変更するようにします。
3. localeが変更された際に、表示するメッセージも更新します。

## マイルストーン3

localStorageを利用して、localeが変更された場合は次回のアクセス時にそのlocaleでサイトが表示されるようにします。

### 要件

1. currentLocaleの設定を更新し、最初にlocalStorage上のデータを読み込み、データが無ければ、デフォルトで"ja"が入るようにしましょう。
2. updateLocaleファンクション内でlocalStorageにlocaleを保存するようにしましょう。

ページにアクセス後ロケールを変更してから、更新ボタンをおしてみましょう。保存されているlcoaleでメッセージが表示されれば成功です。

## 評価

課題の後、以下の２つについてメンターにフィードバックをお願いします。

1. 要件のカバー度: 1.全く出来なかった 2.ほとんど出来なかった 3. 半分ほどは出来た 4.8割ほどは出来た 5. 全部出来た
2. 難易度: 1. とても難しかった 2. 難しかった 3. ちょうど良かった 4. 簡単だった 5. とても簡単だった
