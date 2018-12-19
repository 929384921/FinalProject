# PRD FOR API_ML_AI

## 概述
### 产品简介
Target release|2018/12/31
:---|:---
Epic|一个会说话的菜谱APP
Document status| DRAFT
Document owner| Wu Xindan
Designer/Developer| Wu Xindan
### 产品背景及市场现状
-	市场现状
    - 不少美食APP均兼备做菜教学、美食资讯、购物商城、交流学习等多种功能，深受美食爱好者的追捧。随着多款各具特色的美食APP涌现，该市场呈现出一番稳步发展的格局。 
    - **49%的用户期望通过美食APP交流提升厨艺；**调查数据显示，在使用美食APP的用户中，有49%是喜欢做菜，想通过APP交流提升厨艺，42%想学习做菜，36%的用户想了解三餐营养搭配知识，33%的用户使用美食APP主要是为了方便购买食材。
    - 从速途研究院统计的美食APP评分来看，前五名分别为香哈菜谱、下厨房、网上厨房、豆果美食和美食杰，其中下厨房累计下载量居榜首。
-	产品背景
    - 目前市场上美食APP的菜谱功能以文字+图片+视频为主，虽然比较完善，但在使用过程中，单纯的文字解说无法很好满足用户边做边学的需求。

### 产品目标
目标|具体要求
:---|:----
语音功能|通过添加插件，让用户一边听一边做出美味佳肴或是语音翻页，让用户不用在意沾水的手弄湿手机。
提高用户满足感|通过“命令”让语音进行下一步“教学”，营造出实时教学的交流氛围。（例如：“下一步。”“然后呢？”“好了！”等）


## 功能需求
### 用户使用场景
- 厨房小白，想要自己在家做饭。
- 学生党，在宿舍开小灶
- 上班族，离家一人漂泊，自己下厨吃到家里的味道。
- 想要提升厨艺的人，学习更多菜品制作。
### 产品功能与用户痛点
用户痛点|对应功能|重要性
:---|:---|:---
想要自己做菜但是不知道如何下手/对某样菜品的制作流程不熟悉|菜谱查询功能|很重要
根据菜谱做菜过程中，记不住具体流程|语音合成功能|很重要
做菜的时候手碰到水后不好直接用手翻页|语音翻页功能|次重要
根据菜谱做菜时，有些需要定时的功能需要手动操作，比较麻烦|菜谱自动开启计时功能|次重要

## 产品描述
最小可行性产品：
:---|
利用菜谱API，提供菜谱查询功能|
运用语音合成，将菜谱文字转换成语音，让用户边听边做|

### 人工智能加值

### 人工智能概率性（精确度）

## 原型展示
### 产品架构图
### 产品流程图
### 产品功能原型图

## API使用展示
api列表
:---|
科大讯飞——[语音合成api](https://doc.xfyun.cn/rest_api/%E8%AF%AD%E9%9F%B3%E5%90%88%E6%88%90.html)
聚合数据——[菜谱API](https://www.juhe.cn/docs/api/id/46)

### API输入/输出
- **菜谱API**（通过输入需要查询的菜谱名，获取菜谱信息）
```
#!/usr/bin/python
# -*- coding: utf-8 -*-
import json, urllib
from urllib import urlencode
 
#----------------------------------
# 菜谱大全调用示例代码 － 聚合数据
# 在线接口文档：http://www.juhe.cn/docs/46
#----------------------------------
 
def main():
 
    #配置您申请的APPKey
    appkey = "*********************"
 
    #1.菜谱大全
    request1(appkey,"GET")
 
#菜谱大全
def request1(appkey, m="GET"):
    url = "http://apis.juhe.cn/cook/query.php"
    params = {
        "menu" : "", #需要查询的菜谱名
        "key" : appkey, #应用APPKEY(应用详细页查询)
        "dtype" : "", #返回数据的格式,xml或json，默认json
        "pn" : "", #数据返回起始下标
        "rn" : "", #数据返回条数，最大30
        "albums" : "", #albums字段类型，1字符串，默认数组
 
    }
    params = urlencode(params)
    if m =="GET":
        f = urllib.urlopen("%s?%s" % (url, params))
    else:
        f = urllib.urlopen(url, params)
 
    content = f.read()
    res = json.loads(content)
    if res:
        error_code = res["error_code"]
        if error_code == 0:
            #成功请求
            print res["result"]
        else:
            print "%s:%s" % (res["error_code"],res["reason"])
    else:
        print "request api error"
```
  
  
- **科大讯飞**-语音合成api(通过输入菜谱文本，将文本转换成语音)
```
import base64
import json
import time
import hashlib
import urllib.request
import urllib.parse
# API请求地址、API KEY、APP ID等参数，提前填好备用
api_url = "http://api.xfyun.cn/v1/service/v1/tts"
API_KEY = "b15c3200c6d2f9552a8a2696c31daf32"
APP_ID = "5c1921d5"
OUTPUT_FILE = "C:\\Users\Wxd\Desktop\output.mp3"    # 输出音频的保存路径，请根据自己的情况替换
TEXT = "苟利国家生死以，岂因祸福避趋之"

# 构造输出音频配置参数
Param = {
    "auf": "audio/L16;rate=16000",    #音频采样率
    "aue": "lame",    #音频编码，raw(生成wav)或lame(生成mp3)
    "voice_name": "xiaoyan",
    "speed": "50",    #语速[0,100]
    "volume": "77",    #音量[0,100]
    "pitch": "50",    #音高[0,100]
    "engine_type": "aisound"    #引擎类型。aisound（普通效果），intp65（中文），intp65_en（英文）
}
# 配置参数编码为base64字符串，过程：字典→明文字符串→utf8编码→base64(bytes)→base64字符串
Param_str = json.dumps(Param)    #得到明文字符串
Param_utf8 = Param_str.encode('utf8')    #得到utf8编码(bytes类型)
Param_b64 = base64.b64encode(Param_utf8)    #得到base64编码(bytes类型)
Param_b64str = Param_b64.decode('utf8')    #得到base64字符串

# 构造HTTP请求的头部
time_now = str(int(time.time()))
checksum = (API_KEY + time_now + Param_b64str).encode('utf8')
checksum_md5 = hashlib.md5(checksum).hexdigest()
header = {
    "X-Appid": APP_ID,
    "X-CurTime": time_now,
    "X-Param": Param_b64str,
    "X-CheckSum": checksum_md5
}

# 构造HTTP请求Body
body = {
    "text": TEXT
}
body_urlencode = urllib.parse.urlencode(body)
body_utf8 = body_urlencode.encode('utf8')

# 发送HTTP POST请求
req = urllib.request.Request(api_url, data=body_utf8, headers=header)
response = urllib.request.urlopen(req)

# 读取结果
response_head = response.headers['Content-Type']
if(response_head == "audio/mpeg"):
    out_file = open(OUTPUT_FILE, 'wb')
    data = response.read() # a 'bytes' object
    out_file.write(data)
    out_file.close()
 
In [ ]:
   print('输出文件: ' + OUTPUT_FILE)
else:
    print(response.read().decode('utf8'))
```
输出文件: C:\Users\Wxd\Desktop\output.mp3

### API使用比较

## NOT DONING

## Manifest

