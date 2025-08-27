---
title: MoneyWiz 自动更新国内基金价格
published: 2024-11-02
description: ''
image: ''
tags: [MoneyWiz, Beancount, 记账]
category: '理财'
draft: false 
lang: ''
---

如题，MoneyWiz 虽然能够根据基金代码自动更新基金价格，但是使用的是 yahoo 的 api，不仅链接不稳定，对中国基金的支持也不够好。更糟糕的是，国内基金的代码可能和国外股票代码撞上，导致更新错误价格。

## 更新价格接口

万幸，官方文档[^1]中给出了更新价格的 scheme 规范，理论上只要在 safari 浏览器中输入类似于 `moneywiz://updateholding?symbol={FCODE}.CN&price={dwjz}&date={date}` 的链接即可更新价格。

## 获取价格&自动化脚本

网上基本都是在爬天天基金的数据，本项目自然不会例外，[天天基金 Api](https://kouchao.github.io/TiantianFundApi/apis/#%E8%8E%B7%E5%8F%96%E5%9F%BA%E9%87%91%E5%8E%86%E5%8F%B2%E5%87%80%E5%80%BC) 给出了简便的接口，在本地部署这个项目即可，安装教程见[快速开始](https://kouchao.github.io/TiantianFundApi/guide/)。

为了方便起见，我是在mac上跑的脚本~~，如果没有mac，可以尝试下脚本+捷径的方案？我没试过~~

为了防止和国外股票撞上，给基金代码后面加了 `.CN` 尾缀，这一点需要在 MoneyWiz 记录时注意补上，脚本比较简单，就直接给出来了。

```python  
import webbrowser  
import requests  
import json
import time

pageIndex = 1  
pagesize = 100  
  
tickers = ["002963"]  # 基金代码  
for ticker in tickers:  
    FCODE = ticker  
    resp = requests.get("http://localhost:3000/fundMNHisNetList", params={  
        "FCODE": FCODE,  
        "pageIndex": pageIndex,  
        "pagesize": pagesize  
    })  
  
    if resp.status_code >= 400:  
        continue  
  
    datas = json.loads(resp.content).get("Datas", [])  
    for data in datas:  
        dwjz = data.get("DWJZ", "")  
        if dwjz == "":  
            continue  
        date = data.get("FSRQ", "")  
        if date == "":  
            continue  
        date = date.replace("-", "")  
  
        moneywiz = f"moneywiz://updateholding?symbol={FCODE}.CN&price={dwjz}&date={date}"  
        webbrowser.open(moneywiz)  # 运行  
        time.sleep(1)
```

在结尾，感谢 **[moneywiz-china-funds](https://github.com/log924/moneywiz-china-funds)** 给到的思路。

[^1]: <https://help.wiz.money/en/articles/4525440-automate-transaction-management-with-url-schemas>
