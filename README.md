## 知乎盐选爬虫



### 功能介绍

知乎爬虫，爬取知乎盐选会员小说

通过本项目可以实现，爬取知乎盐选会员里的小说

前提是账号已经开通盐选会员



### 爬取步骤

#### 一、获取cookie

通过谷歌浏览器，打开网址

https://www.zhihu.com/market/paid_column/1315624454782238720/section/1315626212358795264

按F12打开开发者工具

![image-20230220124040584](http://yzwpic.weimayi.cn/img/image-20230220124040584.png)

复制红框部分完整的cookie



打开book.js，修改cookies

将复制的cookies填写上去

```
const cookies = `_ga=GA1.2.915669292.1574093729; q_c1=74385b8ce56a40ccbbfdcc101e35da86|1611739727000|1571844362000; _9755xjdesxxd_=32; YD00517437729195%3AWM_TID=fPZyM8aAGR9FVVQBUUcvzCL1XiJCB%2Fo4; _zap=4ae4d1c2-96fb-403d-92b7-34476b9af323; d_c0=APCXJQ3IxBWPThL5BdIF2mVEvTrAPi5ItWQ=|1666763032; __snaker__id=mCFLYR0ooAaUUlNr; YD00517437729195%3AWM_NI=whamZBeHvyuunG0q0KXmXbKWN%2Bq22BWJvu78db64VoMbBKd78cAgPtzppsjakSNSRaEDkqFBaqM2O5%2FvnAfow2deR7YevtJchvFqKq8SKTZceHHdzcv7iKEgfHyCSHzlYzU%3D; YD00517437729195%3AWM_NIKE=9ca17ae2e6ffcda170e2e6eeb6c873f89bfcd7eb25f38a8aa2c15e929b9a87d56996bd87d6ea6a818dacafe62af0fea7c3b92ab5b8af8ed94aa798ba9af87fae990092b3419cb39883ca5d8ef5bfd3b14a9596ba96b634a8befad5d5658fbe8eace73dfcbd8f88d380bab0c094e96ba98d82b4d16b879ca592c54aa3af83d3ce3fedaaa2a2e565b5eeac86d13d9bbbba95c969acaa8a92ca7bfc8d85b5d969a7988885f969b6e9a7acc86da698b7a4d244bab4979bd837e2a3; _xsrf=da497e0f-8a53-4c5d-a925-eadc714d6baf; Hm_lvt_98beee57fd2ef70ccdd5ca52b9740c49=1674874693,1675992836; z_c0=2|1:0|10:1676601972|4:z_c0|80:MS4xQzRobklnQUFBQUFtQUFBQVlBSlZUWFE0M0dSQURtbG1qbFhTUXF3ZzVxRU5SRWU2ZnJOamtnPT0=|586a435562feb29706295c7fb9c4574682b97250ec63fd8bdc859e6d1ce8d3be; arialoadData=false; q_c1=74385b8ce56a40ccbbfdcc101e35da86|1676864903000|1571844362000; tst=f; Hm_lpvt_98beee57fd2ef70ccdd5ca52b9740c49=1676864905; KLBRSID=53650870f91603bc3193342a80cf198c|1676868976|1676864899`
```



### 二、爬取文章





// 抓取单本书
// 这里的url是这本书的路由地址
// story 为 分类名称
let url = process.argv[2]
let category = process.argv[3]
start(url, 1, category)

执行

``` 正常
node oneBook 'https://www.zhihu.com/xen/market/remix/paid_column/1210518613973028864' 'story' 'romantic'
```

``` 不存在
node oneBook 'https://www.zhihu.com/remix/albums/1309143181594935296' 'story' 'romantic'
```

``` 不存在
node oneBook 'https://www.zhihu.com/xen/market/remix/paid_column/1248616106182778880' 'story' 'romantic'
```

```
node oneBook 'https://www.zhihu.com/xen/market/remix/paid_column/1144205341066739712' 'job' 'market'
```

``` 惊魂倒计时 只拉取到部分文章
node oneBook 'https://www.zhihu.com/xen/market/remix/paid_column/1315624454782238720' 'story' 'suspense'
```



明朝那些事儿全集（2020 版）
1262365258993737728
https://www.zhihu.com/xen/market/remix/paid_column/1262365258993737728


 <!-- https://www.zhihu.com/remix/albums/1309143181594935296 -->
 <!-- 报错 -->


 测试云开发抓包

 'https://www.zhihu.com/xen/market/remix/paid_column/1209068423537557504' 'story' 'anecdote'

"bookId": "1209068423537557504"
"title": "非洲死神埃博拉：让人身体爆炸的「丧尸」病毒"
"title": "被人遗忘的 H1N1，「祖先」病毒曾感染世界 1/3 人口"
"title": "魔幻纪实：我们可能从未真正战胜 SARS"
"title": "鼠疫猖狂：每一次天灾，都是人祸"
"title": "用性病定义艾滋病，人类真的太愚昧了"

测试章节乱序问题
"name": "完美谋杀：一位老刑警笔下的 7 个真实重案故事"
'https://www.zhihu.com/xen/market/remix/paid_column/1187437252308869120' 'story' 'suspense'

















列表页面访问地址
https://www.zhihu.com/market/sort/quality_courses/story?level1=story&level2=suspense

开始爬取
url 为 列表第一页的url接口请求地址，不是页面的地址
comic 为 分类名称

只支持抓取二级分类下的列表页面

故事-漫画'story' 'comic'
```
node index 'https://api.zhihu.com/market/categories/comic?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'person' 'shuping'
```



造假数据
https://www.yezismile.com/book/index
先拉取漫画分类
将bookId改为001 002 003
每本书只留一个章节
修改章节内容




一、悬疑推理'story' 'suspense'
故事-悬疑
'https://api.zhihu.com/market/categories/suspense?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2'
文学-悬疑推理
'https://api.zhihu.com/market/categories/mystery?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2'

二、武侠科幻'story' 'Scifi'
故事-全部
https://api.zhihu.com/market/categories/story?limit=10&dataType=new&level=1&sort_type=hottest&right_type=svip_free&study_type=album

三、奇闻异事'story' 'anecdote'
文学-全部
https://api.zhihu.com/market/categories/literature?limit=10&dataType=new&level=1&sort_type=hottest&right_type=svip_free&study_type=album

四、职场小说'job' 'market'
'https://api.zhihu.com/market/categories/market?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'job' 'market'




从下往上倒着来更新！！！



以下为要抓取的类目

故事-悬疑√
node index 'https://api.zhihu.com/market/categories/suspense?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'suspense'

文学-悬疑推理'literature' 'mystery'，合并到上个分类
node index 'https://api.zhihu.com/market/categories/mystery?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'suspense'

故事-科幻，改为武侠科幻
node index 'https://api.zhihu.com/market/categories/Scifi?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'Scifi'

文学-武侠科幻'literature' 'swordsman'，合并到上个分类
node index 'https://api.zhihu.com/market/categories/swordsman?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'Scifi'

文学-神话传说
node index 'https://api.zhihu.com/market/categories/legends?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'literature' 'legends'

文学-中国文学
node index 'https://api.zhihu.com/market/categories/chinese?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'literature' 'chinese'

文学-人物传记
node index 'https://api.zhihu.com/market/categories/biography?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'literature' 'biography'

故事-历史，改为历史风云
node index 'https://api.zhihu.com/market/categories/history?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'history'

文学-历史风云'literature' 'historical'，合并到上个分类
node index 'https://api.zhihu.com/market/categories/historical?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'history'

故事-奇闻，改为奇闻异事
node index 'https://api.zhihu.com/market/categories/anecdote?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'anecdote'

故事-亲历'story' 'personal-experience'，合并到上个分类
node index 'https://api.zhihu.com/market/categories/personal-experience?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'story' 'anecdote'

职人-职场小说*
node index 'https://api.zhihu.com/market/categories/market?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=2' 'job' 'market'













科学
let pageUrl = 'https://api.zhihu.com/market/categories/science?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'science'

互联网
let pageUrl = 'https://api.zhihu.com/market/categories/network?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'network'

理财
let pageUrl = 'https://api.zhihu.com/market/categories/financial?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'financial'

艺术
let pageUrl = 'https://api.zhihu.com/market/categories/art?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'art'

社科
let pageUrl = 'https://api.zhihu.com/market/categories/social?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'social'

成长
let pageUrl = 'https://api.zhihu.com/market/categories/psychology?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'psychology'

职场
let pageUrl = 'https://api.zhihu.com/market/categories/job?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'job'

教育
let pageUrl = 'https://api.zhihu.com/market/categories/edu?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'edu'

健康
let pageUrl = 'https://api.zhihu.com/market/categories/lifestyle?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'lifestyle'

亲子
let pageUrl = 'https://api.zhihu.com/market/categories/parental?limit=10&dataType=new&sort_type=hottest&study_type=album&right_type=&is_finished=&level=1'
let level1 = 'story2'
let level2 = 'parental'



