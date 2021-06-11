---
name: B站弹幕爬取
about: 爬取弹幕字段与接口不匹配
title: "【提问】{弹幕缺少字段‘total’}"
labels: '提问'
assignees: ''

---

**Python 版本：** 3.8

**模块版本：** 4.1.0

**运行环境：** Windows

---
# 代码
```
verify = Verify(sessdata="28ed4fda%2C1623340975%2C2e16a*c1",csrf="bili_jct")  #个人账号登录信息

file_path = "bili_bv2.csv"
with open(file_path,'r',encoding='utf-8-sig',newline='')as f:
    reader = csv.reader(f)
    reader = list(reader)[1:]
    for r in tqdm(reader):
        index=reader.index(r)
        if index%2==0:
            continue
        #print(index)
        bvi=r[0]
        print(bvi)
        v = video.get_video_info(bvid=bvi) #bvid为视频BV号，从URL中获取
        f = open(r'danmu/%s.txt'%bvi,'w',errors='ignore')
        danmu = video.get_danmaku(bvid=bvi)// 错误发生在这里
        for i in danmu:
            f.write(i.text)
            f.write("\n")
        f.close()
```
# 问题具体描述：
keyError: 'total'
![图片](https://user-images.githubusercontent.com/72337651/121660449-da0c0e00-cad5-11eb-9a3b-d9ed1ccc1626.png)
