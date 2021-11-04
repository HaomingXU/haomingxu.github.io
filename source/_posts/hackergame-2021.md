---
title: 参USTC第八届信息安全大赛(Hackergame 2021)记录
date: 2021-10-30 13:15:22
tags: Daily
permalink: 2021/10/hg2021.html
---

## 0x01 序言
嗯，简单点说，在过去的一周，参与了USTC HG2021，并获得了总排181/2677, 最高1/134, T3一血的成绩。本页内容在于简要记录解题方法，等。

{% asset_img rank0.png 最高排名时截图 %}

<!--more-->
## 0x02 题解

### 签到
没什么好说的, 发现使用GET, 获取Unix时间戳, 直接Google即可。

### 十六进制
使用OCR把16进制数字识别出来后转成ASCII, 即可得出。

### 追寻自由的电波(本题有一血)

打开Premiere, 更改速度/持续时间, 放一遍即可。字母用的是NATO音标, 这是个知识点。

{% asset_img fb.png 一血留念|窝法乙烷 %}

### 猫咪问答
基本上直接搜索相关内容即可。

话说, 那个/dev/null让我懵了好一会...这就是整活吗?

### 卖瓜
多输入几个大数字, 发现在9中输入会溢出, 以此为突破口。

### 透明的文件
考点是ASCII转义, 也就是\033, 不过劣质终端Windows Terminal搭配WSL也显示不出颜色就是了...

### 旅行照片
最大的特征在于海边的肯德基, 故搜索"肯德基 海滩", 发现是新澳海底世界店, 根据百度地图街景与穷举(或者画图)即可得出全部答案。

### 大砍刀
并夕夕红包已入账!

劣质代码如下:
```
using System;
using System.Net;
using System.Text;
using System.Threading;

class dakandao{
    static void Main(string[] args){
        string acturl = "";
        for(int i=0; i<256; i++){
            string ip = i+".0.0.1";
            post(acturl, ip);
            Console.WriteLine(i);
            Thread.Sleep(1000);
        }
    }
    public static void post(string url, string ipaddr){
        WebClient wc = new WebClient();
        wc.Headers.Add("Content-Type", "application/x-www-form-urlencoded");
        wc.Headers.Add("X-Forwarded-For", ipaddr);
        string poststr = "ip="+ipaddr;
        byte[] postdata = Encoding.ASCII.GetBytes(poststr);
        wc.UploadData(url, "POST", postdata);
    }
}
```

### Amnesia 轻度失忆
直接写``printf("Hello, world!");``发现不能输出, 遂搜索.data与.rodata，发现不能使用字符串, 故使用char。

代码如下:
```
int main(void)
{
    char a[13];
    a[0] = 'H';
    a[1] = 'e';
    a[2] = 'l';
    a[3] = 'l';
    a[4] = 'o';
    a[5] = ',';
    a[6] = ' ';
    a[7] = 'w';
    a[8] = 'o';
    a[9] = 'r';
    a[10] = 'l';
    a[11] = 'd';
    a[12] = '!';
    printf(a);
}
```

### 图之上的信息

这道题想了半天没想出来, 后来发现GraphQL有一个introspection, 照抄, 如下:
```
{__type(name: "GUser"){
name
fields(includeDeprecated: true){
name}}}
```

### 阵列恢复带师 RAID 5

用商业软件R-studio直接算出来排序, 数据导出, 直接run一遍.py, 出结果。
