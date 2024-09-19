---
title: Vercel 后端上手
date: 2024-09-19 17:40:40
tags: 学习笔记
categories: 学习笔记
cover: [/img/tj.jpg]
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  banner_text: Hola! This is a article about Python...
toc: true
---
热知识: Vercel 支持后端，可以使用 Flask 语法 （

## 准备工作:

- Flask

- 一个自己的域名

- 一个 Vercel 账号，并且绑定 Github

## 新建文件夹

将文件夹放入以下文件:

- requirements.txt

- vercel.json

- index.py

`requirements.txt`:

```
Flask
requests
pyjson
pyrandom
```

告诉 Vercel 要引入的库，如果要引入其它库请自行搜索。

`vercel.json`

```json
{
  "builds": [
    {
      "src": "./index.py",
      "use": "@vercel/python"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "headers": {
        "cache-control": "no-cache, no-store, must-revalidate",
        "Access-Control-Allow-Origin": "*"
      },
      "dest": "/"
    }
  ]
}
```

`index.py` 以跳转到一个网站为例

```python
from flask import Flask , request , jsonify, redirect, url_for
import requests , json , random
app = Flask(__name__)
app.config['JSON_AS_ASCII'] = False

@app.route('/',methods=["GET"])
def root():
    return redirect('https://www.acerkaio.top/')

```

More...