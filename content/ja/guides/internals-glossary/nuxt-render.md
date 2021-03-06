---
title: 'nuxt.render(req, res)'
description: Node.js サーバーのミドルウェアとして Nuxt.js を使うことができます。
menu: render
category: internals-glossary
position: 10
---

- 型: `Function`
- 引数:
  1. [Request](https://nodejs.org/api/http.html#http_class_http_incomingmessage)
  2. [Response](https://nodejs.org/api/http.html#http_class_http_serverresponse)
- 戻り値: `Promise`

> `nuxt.render` を使うと Node.js サーバーのミドルウェアとして Nuxt.js を使うことができます。

[Express](https://github.com/expressjs/express) と一緒に使う例:

```js
const { loadNuxt, build } = require('nuxt')

const app = require('express')()
const isDev = process.env.NODE_ENV !== 'production'
const port = process.env.PORT || 3000

async function start() {
  // Nuxt インスタンスを取得
  const nuxt = await loadNuxt(isDev ? 'dev' : 'start')

  // すべてのルートを Nuxt.js でレンダリング
  app.use(nuxt.render)

  // ホットリローディングつきの開発モードの場合のみビルド
  if (isDev) {
    build(nuxt)
  }
  // サーバーをリッスン
  app.listen(port, '0.0.0.0')
  console.log('Server listening on `localhost:' + port + '`.')
}

start()
```

<div class="Alert">

ミドルウェアの終わりに `nuxt.render` を呼び出すことをお勧めします。`nuxt.render` は Web アプリケーションのレンダリングを処理し `next()` を呼び出さないからです。

</div>
