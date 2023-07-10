# これは何か
チャット欄に寄せられるコメントに自動で応答をしながら進行をする、AIによるYouTube LIVE配信を行うためのサンプルです。

# 継承元のリポジトリ
https://github.com/k-masashi/sample-chat-ai-vtuber

[makunugiさん](https://github.com/k-masashi)さん、ありがとうございます。

このリポジトリは、上記を改良し、Live2Dモデルとおしゃべりできるようにしたものです。

# 準備

AIによる雑談配信を行うためのソースコードはすでに実装済みです。
下記の準備が必要な項目のみ設定が必要です。

## 1. Live2Dモデル・背景画像の用意
背景画像を変更したい場合、`background.png`の画像を別の画像に差し替えてください。

Live2Dモデルを変更したい場合、ルートディレクトリにLive2Dモデルのファイルを設置し、`aivtuber.js`の下記の箇所に入力してください。

```js
const modelPath = '<モデルディレクトリ内のmodel3.jsonファイルへのパスを入力してください>';
```

## 2. meboのAPIキー・エージェントIDの設定
[mebo](https://mebo.work)を利用して、会話が可能なAIキャラクターを作成してください。
mebo内の[Chara.AI Generator](https://zenn.dev/makunugi/articles/ebecbb5de562d6)という機能を利用すると、スムーズにAIキャラクターが作成できます。

AIキャラクターを作成したら、meboの公開設定画面でAIキャラクターを限定公開し、「APIを有効化」してください。

APIを有効化するとAPIキーとエージェントIDを取得できます。

APIキーを取得したら、`aivtuber.js`を開き、下記の箇所にAPIキーとエージェントIDを入力しましょう。

```js
const MEBO_API_KEY = "<meboのAPIキーを入力してください。>";
const MEBO_AGENT_ID = "<meboのAgent IDを入力してください。>";
```

## 3. VOICEVOXをインストール
声の読み上げはVOICEVOXを利用します。
下記からVOICEVOXをインストールし、起動してください。VOICEVOXが起動されることで、ローカル環境にAPIが立ち上がります。
[VOICEVOX公式サイト](https://voicevox.hiroshiba.jp/)


```js
const VOICE_VOX_API_URL = "http://localhost:50021";
```
デフォルトで上記が`aivtuber.js`に設定されています。ポート番号を変更する際は、上記のURLを適宜変更してください。

尚、VOICEVOXを利用してYouTube配信をする場合は、ライセンス表記が必要です。概要欄などできちんと明記をして利用しましょう。
[VOICEVOX利用規約](https://voicevox.hiroshiba.jp/term/)

## 4. YouTubeライブ配信のVIDEO IDを設定
YouTubeのライブ配信の準備が整ったら、ライブ配信の動画のURLに末尾にあるVideo IDを`aivtuber.js`の下記の箇所に入力してください。

```js
const YOUTUBE_VIDEO_ID = '<YouTube Video IDを入力してください。>';
```

Video IDは動画のURLの末尾にある「v=」より後の文字列です。
`https://www.youtube.com/watch?v=x12345667`
上記であれば、Video IDは「x12345667」になります。


## 5. YouTube Data APIのAPIキーの用意
YouTubeライブ配信のコメントを取得するため、YouTube Data APIのAPIキーを利用します。
APIキーの取得方法は、[こちら](https://qiita.com/shinkai_/items/10a400c25de270cb02e4#:~:text=%E8%AA%8D%E8%A8%BC%E6%83%85%E5%A0%B1%E3%81%AE%E4%BD%9C%E6%88%90%EF%BC%88API%E3%82%AD%E3%83%BC%E3%81%AE%E4%BD%9C%E6%88%90%EF%BC%89,-%E3%80%8C%E8%AA%8D%E8%A8%BC%E6%83%85%E5%A0%B1%E3%80%8D%E3%82%92&text=%E3%80%8C%E8%AA%8D%E8%A8%BC%E6%83%85%E5%A0%B1%E3%82%92%E4%BD%9C%E6%88%90%E3%80%8D%E3%82%92,%E4%BF%9D%E5%AD%98%E3%80%8D%E3%82%92%E3%82%AF%E3%83%AA%E3%83%83%E3%82%AF%E3%81%97%E3%81%BE%E3%81%99%E3%80%82)の記事が大変わかりやすくまとめられていました。

APIキーを取得したら、`aivtuber.js`の下記の箇所に入力しましょう。

```js
const YOUTUBE_DATA_API_KEY = '<YouTube Data APIのAPIキーを入力してください。>';
```

# 動作確認
`index.html`をブラウザで開きましょう。
ページ下部のテキスト入力欄にコメントを入力し「送信」ボタンを押して、無事応答が返ってくれば成功です。

# LIVE開始
動作確認が完了したら、「LIVE開始」を押しましょう。
YouTube LIVEのコメントに対して応答を返すようになります。

[OBS](https://obsproject.com/ja/download)などの画面配信が可能なツールを利用して、AI VTuberを表示しているブラウザのキャプチャをYouTubeに配信しましょう。
- [解説1 (OBS-Youtube連携)](https://youtu.be/s9ZZAgcLRpY?t=1295)
- [解説2 (配信設定)](https://youtu.be/s9ZZAgcLRpY?t=1899)

環境によっては、複数出力装置の設定が必要な場合があります。
AITuberの音がYoutubeで流れないなどの場合、[Youtube解説](https://youtu.be/s9ZZAgcLRpY?t=1644)を参考に、設定をお願いします。

## License

The code in this project is licensed under MIT license. See the [LICENSE](LICENSE) file in this repository.

However, files located in the '/Uniform01_39' directory are a separate matter. These files are proprietary and their reproduction, modification, distribution, or use in any way is strictly forbidden without explicit permission. For more information, see the [LICENSE](Uniform01_39/LICENSE) file in the 'Uniform01_39' directory.
