# 本地环境配置 HTTPS 证书

* mkcert 是一个用 GO 写的零配置专门用来本地环境 https 证书生成的工具

```
# 本地安装 CA
$ mkcert -install
Created a new local CA at "/Users/shanyue/Library/Application Support/mkcert" 💥
The local CA is now installed in the system trust store! ⚡️
The local CA is now installed in the Firefox trust store (requires browser restart)! 🦊

$ mkcert local.shanyue.tech
Using the local CA at "/Users/xiange/Library/Application Support/mkcert" ✨

Created a new certificate valid for the following names 📜
 - "local.shanyue.tech"

The certificate is at "./local.shanyue.tech.pem" and the key at "./local.shanyue.tech-key.pem" ✅

```

* 通过 cert 最终会成功安装 CA，并生成 cert 及 key，文件目录如下

```
{
  cert: './local.shanyue.tech.pem',
  key: './local.shanyue.tech-key.pem'
}
```

* 在 webpack 中配置 https
```
module.exports = {
  //...
  devServer: {
    https: true,
    key: fs.readFileSync('/path/to/server.key'),
    cert: fs.readFileSync('/path/to/server.crt')
  }
};

```

* 在 node server 中配置 https

```
import path from 'path'
import fs from 'fs'
import express from 'express'
import http from 'http'
import https from 'https'

const app = express();

const cred = {
  key: fs.readFileSync(path.resolve(__dirname, '../key.pem')),
  cert: fs.readFileSync(path.resolve(__dirname, '../cert.pem'))
}
const httpServer = http.createServer(app)
const httpsServer = https.createServer(cred, app)

httpServer.listen(8000);
httpsServer.listen(8888);

```

* 而对于 webpack-dev-server，仔细阅读源码就能过发现它的原理也是如此，详见代码 webpack-dev-server:/lib/Server.js

```
const http = require('http');
const https = require('https');

if (this.options.https) {
  if (semver.gte(process.version, '10.0.0') || !isHttp2) {
    this.listeningApp = https.createServer(this.options.https, this.app);
  } else {
    // The relevant issues are:
    // https://github.com/spdy-http2/node-spdy/issues/350
    // https://github.com/webpack/webpack-dev-server/issues/1592
    this.listeningApp = require('spdy').createServer(
      this.options.https,
      this.app
    );
  }
} else {
  this.listeningApp = http.createServer(this.app);
}

```