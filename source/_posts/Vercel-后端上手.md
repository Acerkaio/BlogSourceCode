---
title: Vercel 后端上手
date: 2024-09-19 17:40:40
tags: 记录
categories: 记录
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

## 实现随机图

```python
from flask import Flask , request , jsonify, redirect, url_for
import requests , json , random
app = Flask(__name__)
app.config['JSON_AS_ASCII'] = False

@app.route('/',methods=["GET"])
def root():
    return redirect('https://pixiv.acerkaio.top/')

@app.route('/rd',methods=["GET"])

def rdom():

    url = f'https://data.acerkaio.top/elaina.json' #改成你的 url
    

    header = {'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) '
                            'Chrome/112.0.0.0 Safari/537.36',
            'cookie': '__yjs_duid=1_b1ac9fc87dce4de5552d7cf0924fb4981686228951567; u=b0281776fd75d3eefeb3562b2a5e6534; '
                        '__bid_n=1889b14047a51b2b754207; '
                        'FPTOKEN=qU+ieOMqkW6y6DlsOZ+D/T'
                        '+SCY6yS3dYvGXKibFoGBijKuUuSbc3ACFDzjlcC18wuDjNLENrw4ktAFAqnl3Akg492Lr4fbvNrkdJ'
                        '/ZQrluIdklkNDAKYnPrpcbe2H9y7AtX+/b+FCTkSTNv5+qB3OtQQ3BXXsEen72oEoAfK+H6'
                        '/u6ltZPdyHttJBJiXEDDS3EiUVt+S2w+8ozXENWbNt/AHeCgNUMmdeDinAKCR+nQSGK/twOoTLOU/nxBeSAazg'
                        '+wu5K8ooRmW00Bk6XAqC4Cb829XR3UinZHRsJxt7q9biKzYQh'
                        '+Yu5s6EHypKwpA6RPtVAC1axxbxza0l5LJ5hX8IxJXDaQ6srFoEzQ92jM0rmDynp+gT'
                        '+3qNfEtB2PjkURvmRghGUn8wOcUUKPOqg==|mfg5DyAulnBuIm/fNO5JCrEm9g5yXrV1etiaV0jqQEw=|10'
                        '|dcfdbf664758c47995de31b90def5ca5; PHPSESSID=18397defd82b1b3ef009662dc77fe210; '
                        'Hm_lvt_de3f6fd28ec4ac19170f18e2a8777593=1686322028,1686360205; '
                        'history=cid%3A2455%2Ccid%3A2476%2Ccid%3A5474%2Ccid%3A5475%2Ccid%3A2814%2Cbid%3A3667; '
                        'Hm_lpvt_de3f6fd28ec4ac19170f18e2a8777593=1686360427'}

    response = requests.get(url, headers=header)
    text = response.text
    res = json.loads(text)
    number = random.randint(0,(len(res) - 1))
    result = res[number]
    fina_res = json.dumps(result,ensure_ascii=False)

    return json.loads(fina_res)
```