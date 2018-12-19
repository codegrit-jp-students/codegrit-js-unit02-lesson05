## ブラウザの対応状況を調べる

さて、ここまでのレッスンではブラウザ対応についてはあまり触れてきませんでした。しかし実際にはLocal Storageのような仕組みはブラウザによっては対応がされていない場合もあります。例えば、レッスン3で学んだFetchも同様で対応済みのブラウザとそうでないものがあります。ここでは、こうしたブラウザごとの対応をするための基本を学んでいきましょう。

### "Can I use"を利用する

Can I useというサイトでは、利用しようとしているAPIがどのブラウザで対応済みかどうかを簡単に確認することが出来ます。

例えば、2018年2月現在、Fetch APIのブラウザごとの対応状況は以下のようになっています。

![Can I use - Fetch](./images/caniuse-fetch.png)

ご覧の通り、Fetch APIはIE11ではFetch APIが実装されていないことが分かります。IE11のシェアは日本国内ではまだ20%以上なので、Fetch APIをそのまま使ってしまうと、サービスによっては20%あるいはそれ以上のユーザーがサービスを使えないという自体に陥ってしまいます。

### Polyfillを使う

こうした一部のブラウザへ対応するために、NPM上にはPolyfillと呼ばれるパッケージが公開されています。例えば、whatwg-fetchというライブラリはその一つです。

- [whatwg-fetch](https://github.com/github/fetch)

```javascript
import fetch from 'whatwg-fetch';

fetch(...); // polyfillを利用することで、未対応のブラウザでもfetchが利用可能となる。
```

### メッセージを表示する

APIによってはpolyfillを利用しても対応が出来ない場合があります。例えばWebRTC APIはブラウザ間でSkypeのようなビデオ通話を行うことを可能にします。しかし、現状ではChromeやFirefoxを除くと対応が不十分です。こうした場合にはそのAPIが実装されているかどうかを調べ、未対応ならそれに対応するメッセージを表示するというような対応が必要です。

```javascript

if (window.RTCPeerConnection) {
  // WebRTCのRTCPeerConnectionが利用可能。
} else {
  // 未対応
}

```

## 更に学ぼう

- [HTTP Cookie - Mozilla](https://developer.mozilla.org/ja/docs/Web/HTTP/Cookies)
- [Web Storage API - Mozilla](https://developer.mozilla.org/ja/docs/Web/API/Web_Storage_API)