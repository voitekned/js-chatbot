# client

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

App.vueについての解説↓

このコードは、Vue.jsのコンポーネントです。このコンポーネントは、クライアントとサーバー間のチャットボットアプリケーションを実装します。

messagesは、サーバーとのやりとりを保存する配列のリファレンスです。
messageContentは、入力フォームに入力されたテキストメッセージを保存するリファレンスです。
sendMessage関数は、フォームが送信されたときに呼び出されます。この関数は、createMessage関数を呼び出してメッセージを作成し、getResponse関数を呼び出してサーバーからのレスポンスを取得します。
createMessage関数は、新しいメッセージを配列に追加するものです。
getResponse関数は、POSTリクエストを送信してサーバーからのレスポンスを取得します。レスポンスは、createMessage関数を使って保存されます。
このコンポーネントのセットアップ関数は、これらのリファレンスと関数を返します。

以下により詳しい仕様を記載

このコンポーネントでは、Vue.jsのref APIを使用して、コンポーネント内で使用する変数（messagesとmessageContent）を管理しています。

messagesリファレンスは、クライアントとサーバー間のやりとり（メッセージ）を保存する配列です。この配列は、Vue.jsのtemplateセクションで反復処理して表示されます。

messageContentリファレンスは、入力フォームに入力されたテキストメッセージを保存する変数です。

sendMessage関数は、フォームが送信されたときに呼び出されます。この関数は、まずmessageContent.valueが空でないことを確認します。次に、createMessage関数を呼び出して、入力されたメッセージを配列に追加します。最後に、getResponse関数を呼び出して、サーバーからのレスポンスを取得します。

createMessage関数は、新しいメッセージを配列に追加するものです。この関数は、配列内の最後の要素のIDを取得して、新しいメッセージに対して一意のIDを割り当てます。最後に、配列に新しいメッセージを追加します。

getResponse関数は、Axiosライブラリを使用して、POSTリクエストを送信してサーバーからのレスポンスを取得します。この関数は、POSTリクエストのボディに、入力されたメッセージを含むオブジェクトを渡します。サーバーからのレスポンスは、createMessage関数を呼び出して、配列に保存されます。

このコンポーネントのセットアップ関数は、これらのリファレンスと関数を返します。これにより、テンプレートとScriptセクションでこれらの変数と関数を使用


app.jsについての解説↓
このコードは、Node.jsのExpressフレームワークを使用してWebサーバーを構築するものです。このWebサーバーは、クライアントからのPOSTリクエストを受信し、そのボディ内のテキストメッセージをCleverbotAPIに送信し、APIからのレスポンスを返すという単純なチャットボットアプリケーションです。サーバーは、ポート8000で動作しており、サーバー起動時に「running」というメッセージがコンソールに表示されます。



