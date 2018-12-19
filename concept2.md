## Web Storage

以前はブラウザ上にデータを保存する方法はCookieしかありませんでした。Cookieでは、データが必ずHTTPヘッダーに含まれてサーバーに送信されるため、一回一回の送信のデータ量が増えてしまう点や、保存出来るデータ量が最大4kb程度と少ないことなど欠点がありました。Web Storageはこうした欠点をおぎなうために生まれました。Web Storageでは、一般的に5MB以上の大きなデータを保存することが可能です。(保存できる容量はブラウザにより異なります。)

### Local StorageとSession Storage

Web Storageには、Session StorageとLocal Storageの２つがあります。基本的な利用方法はほとんど同じですがLocal Storageがクライアント側で消去しない限り半永久的に残り続ける(Local StorageにはCookieと異なり期限という概念がありません。)のに対し、Session Storageは、一回のセッションでのみ有効という特徴があります。そのため、Session Storageは異なるブラウザタブ上でも共有されません。

### Web Storageを利用する

1. データを保存する。

データを保存するにはsetItemメソッドを利用します。

```javascript
let myData = {
  userId: 1,
  email: "info@example.com",
  role: "admin"
}

localStorage.setItem('myData', myData);
```

2. データを取得する。

データの取得にはgetItemメソッドを利用します。

```javascript
let readData = localStorage.getItem('myData');
console.log(readData); 
/* 
{
  userId: 1,
  email: "info@example.com",
  role: "admin"
}
*/
```

3. 保存されたデータを消去する

保存したデータをキーごと消去するにはremoveItemメソッドを利用します。

```javascript
localStorage.removeItem('myData');
let readData = localStorage.getItem('myData');
console.log(readData); // => null
```

4. localStorageに保存されている全てのデータを消去する

localStorage内のすべてのデータを消去するにはclearメソッドを利用します。

```javascript
localStorage.setItem('data1', "test");
localStorage.setItem('data2', {message: "test"});

localStorage.celar();

localStorage.getItem('data1'); // => null
localStorage.getItem('data2'); // => null
```

### Session Storageの使い所

Session Storageは例えばですが、アプリケーション上の異なるページ間で共有したいデータがある場合に利用できます。例えばですが、他のユーザーへメッセージを送信するアプリケーションで、書きかけの情報を保存しておきたいことを考えましょう。

この時、以下のようなことが出来ます。

```javascript
let mailData1 = {
  receiverId: 1
  message: "これはユーザー1宛ての書きかけのメッセージです。"
}

let mailData2 = {
  receiverId: 1
  message: "これはユーザー2宛ての書きかけのメッセージです。"
}

sessionStorage.setItem('messages-user-1', mailData1);
sessionStorage.setItem('messages-user-2', mailData2);

// メッセージ画面を開いた時に下書きがないかどうか確認する。

sessionStorage.getItem('messages-user-1'); // => mailData1が得られる。
```

このようにして、他のページに移動した後に、再度ユーザー１へのメッセージを編集するページを開いた時でも書きかけのメッセージを表示することが出来ます。タブを閉じれば、こうした下書きは消えます。

### Local Storageの利用期限

上述の通りLocal Storageには期限(expiration)という概念がありません。そのため、Local Storageに保存するデータの利用期限を設定したい場合は、例えば保存するデータ上にその情報を含める必要があります。また、Local Storageはクライアント側で操作することが出来るので、場合によってはレッスン5上で紹介するJWTなどを利用して暗号化して、サーバー側のみで情報を操作出来るようにするということが必要となります。

```javascript
const forteenDays = 14 * 24 * 60 * 60 * 1000; // 14日間をミリ秒で換算したもの

let data = {
  expiry: (Date.now() + forteenDays),
  message: "14日後に期限が来るデータ"
}

localStorage.setItem('some-data', data);

// データを読み取る

let readData = localStorage.getItem('some-data');
if (readDate !== null) {
  if (readData.expiry - Date.now() >= 0) {
    // 有効
  } else {
    // 期限切れのため、データを消去する。
    localStorage.removeItem('some-data');
  }
}
```
