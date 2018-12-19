## HTTP通信はステートレス

レッスン3ではHTTP通信についての基本を学びました。HTTPについて注意しておいて頂きたいのはHTTPはステートレス(状態を保持しない)なプロトコルということです。これはどういうことかというと、例えば多くのサイトではユーザーの認証を行いますが、一度ユーザーの認証が行われたとしてもその情報はHTTP通信には反映される仕組みがなく、ブラウザ側でそれを記憶する必要があるということです。そのために利用されるのがこれから解説を行う、Cookie、Local Storage、Session Storageといった仕組みです。

## Cookie

Cookieとは、サーバーがブラウザへと送信するデータです。ブラウザは受け取ったCookieを保存し、HTTPリクエストを送信する際にHTTPヘッダーに含めて送信されます。Cookieは約4KBまでしかデータを保存することが出来ないという、制限があるため用途は制限されます。Cookie情報は同じTLD(トップレベルドメイン)の場合、サブドメイン間で共有することが可能です。

### Cookieをクライアントサイドで保存する

Cookieはjs-cookieのようなNPMパッケージを利用することで操作することが出来ます。

```javascript
import Cookies from 'js-cookie';

Cookies.set('locale', 'ja-JP'); // ユーザーの使用言語に日本語を指定
```

上記の例のように、localeを設定することでアプリの表示言語をユーザーに併せて変更することなどが可能となります。

### Cookieの利用期限を指定する

Cookieの利用期限を指定することも出来ます。例えば、Webサービスにログインする際に「ログイン状態を維持する」というようなチェックボックスを見たことがあると思います。これはCookieの利用期限を指定することで実現出来ます。例えば、2週間後にCookieが切れるようにしたい場合は以下のようにします。

```javascript
import Cookies from 'js-cookie';

Cookies.set('locale', 'ja-JP', { expires: 14 }); // 14日後に期限切れとなる。
```

### Cookieをサブドメイン間で共有する

上述の通り、Cookieはサブドメイン間で共有できるという特徴があります。そのため、Cookieを使うことで、`www.example.com`というドメイン上でログインしていれば、`blog.example.com`のようなサブドメインのページ内でもログインした状態を保つことが出来ます。これを実現するには以下のようにします。

```javascript
import Cookies from 'js-cookie';

Cookies.set('locale', 'ja-JP', { expires: 14, domain: 'example.com' }); // サブドメイン間で共有
Cookies.set('locale', 'ja-JP', { expires: 14, domain: 'www.example.com' }); // 一つのサブドメインに限定する
```

### Cookieの送信をhttps(SSL/TLS)利用時のみに制限する

Cookieの送信をSSL/TLS通信上に限定したい場合には以下のようにします。

```javascript
import Cookies from 'js-cookie';

Cookies.set('locale', 'ja-JP', { secure: true });
```