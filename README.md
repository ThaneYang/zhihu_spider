## 知乎盐选爬虫


### 功能介绍

知乎爬虫，爬取知乎盐选会员小说

通过本项目，可以实现在微信小程序端爬取知乎盐选VIP会员里的小说

前提是账号已经开通盐选会员



### 技术栈

微信小程序

Uniapp应用框架

小程序云开发



### 爬取步骤

#### 一、获取cookie

通过谷歌浏览器，打开网址

https://www.zhihu.com/market/paid_column/1315624454782238720/section/1315626212358795264

按F12打开开发者工具

![image-20230220124040584](http://yzwpic.weimayi.cn/img/image-20230220124040584.png)

复制红框部分完整的cookie



打开pages/catchBook/catchOneBook.js，修改cookies

将复制的cookies填写上去

```
const cookies = `_ga=GA1.2.915669292.1574093729; q_c1=74385b8ce56a40ccbbfdcc101e35da86|1611739727000|1571844362000; _9755xjdesxxd_=32; YD00517437729195%3AWM_TID=fPZyM8aAGR9FVVQBUUcvzCL1XiJCB%2Fo4; _zap=4ae4d1c2-96fb-403d-92b7-34476b9af323; d_c0=APCXJQ3IxBWPThL5BdIF2mVEvTrAPi5ItWQ=|1666763032; __snaker__id=mCFLYR0ooAaUUlNr; YD00517437729195%3AWM_NI=whamZBeHvyuunG0q0KXmXbKWN%2Bq22BWJvu78db64VoMbBKd78cAgPtzppsjakSNSRaEDkqFBaqM2O5%2FvnAfow2deR7YevtJchvFqKq8SKTZceHHdzcv7iKEgfHyCSHzlYzU%3D; YD00517437729195%3AWM_NIKE=9ca17ae2e6ffcda170e2e6eeb6c873f89bfcd7eb25f38a8aa2c15e929b9a87d56996bd87d6ea6a818dacafe62af0fea7c3b92ab5b8af8ed94aa798ba9af87fae990092b3419cb39883ca5d8ef5bfd3b14a9596ba96b634a8befad5d5658fbe8eace73dfcbd8f88d380bab0c094e96ba98d82b4d16b879ca592c54aa3af83d3ce3fedaaa2a2e565b5eeac86d13d9bbbba95c969acaa8a92ca7bfc8d85b5d969a7988885f969b6e9a7acc86da698b7a4d244bab4979bd837e2a3; _xsrf=da497e0f-8a53-4c5d-a925-eadc714d6baf; Hm_lvt_98beee57fd2ef70ccdd5ca52b9740c49=1674874693,1675992836; z_c0=2|1:0|10:1676601972|4:z_c0|80:MS4xQzRobklnQUFBQUFtQUFBQVlBSlZUWFE0M0dSQURtbG1qbFhTUXF3ZzVxRU5SRWU2ZnJOamtnPT0=|586a435562feb29706295c7fb9c4574682b97250ec63fd8bdc859e6d1ce8d3be; arialoadData=false; q_c1=74385b8ce56a40ccbbfdcc101e35da86|1676864903000|1571844362000; tst=f; Hm_lpvt_98beee57fd2ef70ccdd5ca52b9740c49=1676864905; KLBRSID=53650870f91603bc3193342a80cf198c|1676868976|1676864899`
```



#### 二、小程序项目的搭建

通过HbuilderX，新建项目，勾选云开发

![image-20230223093518697](http://yzwpic.weimayi.cn/img/image-20230223093518697.png)



将uniCloud下的cloudfunctions和database两个目录拷贝到本地新建的项目uniCloud中

![image-20230223093710494](http://yzwpic.weimayi.cn/img/image-20230223093710494.png)



将pages/catchBook拷贝到本地新建的pages目录中，同时在pages.json中添加该页面路径

![image-20230223093910606](http://yzwpic.weimayi.cn/img/image-20230223093910606.png)



运行小程序项目

![image-20230223094012740](http://yzwpic.weimayi.cn/img/image-20230223094012740.png)



打开catchBook页面

![image-20230223094120906](http://yzwpic.weimayi.cn/img/image-20230223094120906.png)







#### 三、开始爬取

点击”爬取一本书“，爬取某一本知乎盐选上的小说

https://www.zhihu.com/xen/market/remix/paid_column/1350774263411064832

![image-20230223120027633](http://yzwpic.weimayi.cn/img/image-20230223120027633.png)





点击”爬取列表“，则爬取某个分类下的小说，按页码来爬取，比如爬取第一页的10条

https://www.zhihu.com/xen/market/vip/remix-album

![image-20230223115225882](http://yzwpic.weimayi.cn/img/image-20230223115225882.png)








