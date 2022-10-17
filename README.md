# 作业内容

## Project1: 大规模爬虫

### 爬虫模块
+ Semantic Scholar：[https://www.semanticscholar.org](https://www.semanticscholar.org/)
  + 含标题、作者、摘要、图表、引文、相关论文等信息
  + [sample here](https://www.semanticscholar.org/paper/Attention-is-All-you-Need-Vaswani-Shazeer/204e3073870fae3d05bcbc2f6a8e263d9b72e776)
+ arXiv: [https://arxiv.org](https://arxiv.org/)
  + 含标题、作者、摘要、PDF、latex文档等信息。
  + [sample here](https://arxiv.org/abs/1406.2661)
+ ScienceDirect：[https://www.sciencedirect.com](https://www.sciencedirect.com/)
  + 含作者、摘要、关键词等论文相关信息
  + [sample here](https://www.sciencedirect.com/science/article/abs/pii/S0004370221001314)
#### 要求

+ **Semantic Scholar 必选**
+ **arXiv** 和 **ScienceDirect 二选一**
+ **ScienceDirect** 爬虫任务的论文领域要求包含**多领域**的数据
+ 爬到的数据必须存储到 [MongoDB](https://www.mongodb.com) 中，字段定义详见`db_fields.md`
+ 数据源越丰富越好，当从不同数据源爬取到相同论文时，需要**去除重复数据**
+ 从每个数据源获取的数据需要具有**完备性**，即爬取数据量占全站数据量的比例越高越好。

+ 要求搭建一个完整的**爬虫框架**，在爬取不同的数据源时，只需要根据实际情况，手写少量解析网页的部分，即数据源是可插拔的。此处推荐 [Python Scrapy爬虫库](https://scrapy.org)
+ 要求实现**增量式**爬取，定时更新
+ 要求爬虫至少采用如下技术手段：
  + 当爬取一个规模较大的网站时，采用某种策略/顺序，保证爬取结果不重不漏
  + 使用多线程/多进程等技术提升爬虫效率
  + 使用ip池、调整等待时间等技术抵御网站反爬
  + 如果网络崩溃，能够从断点续爬
  + 使用日志技术实时展示爬取进度
+ 搭建一个基本的 [Elasticsearch](https://www.elastic.co/) + [Kibana](https://www.elastic.co/cn/kibana/) 检索系统，对爬取的数据建立索引，方便展示



## Project2: 论文标签检索引擎

### 爬虫模块

#### 推荐爬取的站点
+ Paperwithcode: [https://paperswithcode.com](https://paperswithcode.com/)

#### 要求

+ 爬取论文所用数据集、论文提及方法等信息
+ 爬到的数据必须存储到 **MongoDB** 中，字段必须定义清晰

### 检索模块

#### 要求

+ 从MongoDB中读取数据实现**综合检索**，要求无论是输入`任务名称`、`评价指标`、`论文题目`、`论文方法`、`论文数据集`，都能得到相应的检索结果，如下例所示：

[![xNHo2q.png](https://s1.ax1x.com/2022/10/11/xNHo2q.png)](https://imgse.com/i/xNHo2q)


+ 可以自己实现搜索算法，也可以使用已有的搜索引擎工具，比如[Elasticsearch](https://www.elastic.co/)
+ 要求展示模块提供`任务名称网络信息`、`评价指标网络信息`、`论文题目网络信息`、`论文方法网络信息`、`论文数据集网络信息`

### 展示模块

#### 要求

+ 设计并实现一个论文标签检索引擎网站，包括三个页面：

  + 首页/搜索页

  + 检索结果列表页
  
    + 上述五项任务分开展示

    + 可选加分项：
      + 根据标签网络计算每个标签的重要性分数并展示
      + 构建`任务名称`、`评价指标`、`论文题目`、`论文方法`、`论文数据集`的**可视化知识图谱**（或者任选其中几项构建知识图谱）    
      + 其他有创意的趣味展示

+ 推荐使用 [Python Django](https://www.djangoproject.com/) 库来实现


### 提交内容

+ 一个**MongoDB**数据库
+ 在仓库`README`中给出爬取数据的**统计信息**，例如每个数据源爬取的标签数、字段覆盖率等

+ 验收时，展示论文标签检索引擎的检索结果



## Project3: 基于全文信息的论文检索引擎

除对论文的题目摘要等信息进行检索外，对论文全文内容进行深度检索。

### 数据处理模块
+ 在 [Github](https://drive.google.com/file/d/1xC-K6__W3FCalIDBlDROeN4d4xh0IVry/view?usp=sharing) 上下载ACL语料库 (`3.6GB`)，并把xml格式转化成全文文本并储存在数据库中。

### 检索模块
+ 搭建 **Elasticsearch** 实现从某一个或若干字段检索
+ 检索时要求同时考虑 `论文题目`，`摘要`，`论文全文` 等信息，并保证 **检索效率**
+ 能结合 **具体案例** 分析说明满足第二点要求
+ 解释说明全文检索的 **方法原理**

### 展示模块

- 设计并实现一个学术论文搜索引擎网站，包括三个页面

  - 首页/搜索页
  - 检索结果列表页
  + 论文详情页面：
    + 包含论文标题、摘要、参考文献等相关信息

- 展示样例如下图所示：
  
[![xNHIGn.png](https://s1.ax1x.com/2022/10/11/xNHIGn.png)](https://imgse.com/i/xNHIGn)
- 推荐使用 [Python Django](https://www.djangoproject.com/) 库来实现

#### 提交内容
+ 一个**MongoDB**数据库，包含`论文标题`、`摘要`、`全文信息`等重要性字段
+ 展示基于全文信息的论文检索引擎的检索结果，并能 **结合具体案例** 说明全文信息对检索结果的影响以及 **检索效率** 的提升
+ 展示可视化搜索引擎# 作业内容

## Project1: 大规模爬虫

### 爬虫模块
+ Semantic Scholar：[https://www.semanticscholar.org](https://www.semanticscholar.org/)
  + 含标题、作者、摘要、图表、引文、相关论文等信息
  + [sample here](https://www.semanticscholar.org/paper/Attention-is-All-you-Need-Vaswani-Shazeer/204e3073870fae3d05bcbc2f6a8e263d9b72e776)
+ arXiv: [https://arxiv.org](https://arxiv.org/)
  + 含标题、作者、摘要、PDF链接、latex文档等信息。
  + [sample here](https://arxiv.org/abs/1406.2661)
+ ScienceDirect：[https://www.sciencedirect.com](https://www.sciencedirect.com/)
  + 含标题、作者、摘要、关键词、PDF链接等论文相关信息
  + [sample here](https://www.sciencedirect.com/science/article/pii/S2090123221001491)
#### 要求

+ **Semantic Scholar** 爬虫任务的图表需下载到本地并将本地路径存储在数据库中
+ 爬取PDF链接、latex文档时需验证是否**可下载**，并下载一定量的论文以表明爬虫代码具有下载能力
+ **ScienceDirect** 爬虫任务的论文领域要求包含**多领域**的数据
+ 爬到的数据必须存储到 [MongoDB](https://www.mongodb.com) 中，字段定义详见`db_fields.md`
+ 数据源越丰富越好，当从不同数据源爬取到相同论文时，需要**去除重复数据**
+ 从每个数据源获取的数据需要具有**完备性**，即爬取数据量占全站数据量的比例越高越好。
+ 要求搭建一个完整的**爬虫框架**，在爬取不同的数据源时，只需要根据实际情况，手写少量解析网页的部分，即数据源是可插拔的。此处推荐 [Python Scrapy爬虫库](https://scrapy.org)
+ 要求实现**增量式**爬取，定时更新
+ 要求爬虫至少采用如下技术手段：
  + 当爬取一个规模较大的网站时，采用某种策略/顺序，保证爬取结果不重不漏
  + 使用多线程/多进程等技术提升爬虫效率
  + 使用ip池、调整等待时间等技术抵御网站反爬
  + 如果网络崩溃，能够从断点续爬
  + 使用日志技术实时展示爬取进度
+ 搭建一个基本的 [Elasticsearch](https://www.elastic.co/) + [Kibana](https://www.elastic.co/cn/kibana/) 检索系统，对爬取的数据建立索引，方便展示

### 提交内容

+ 一个**MongoDB**数据库
+ 在仓库`README`中给出爬取数据的**统计信息**，例如每个数据源爬取的标签数、字段覆盖率等
+ 验收时，展示检索结果



## Project2: 论文标签检索引擎

### 爬虫模块

#### 推荐爬取的站点
+ Paperwithcode: [https://paperswithcode.com](https://paperswithcode.com/)

#### 要求

+ 爬取论文标题等基本信息及其所属任务、数据集、提及方法、baseline等相关信息
+ 爬到的数据必须存储到 **MongoDB** 中，字段必须定义清晰

### 检索模块

#### 要求

+ 从MongoDB中读取数据实现**综合检索**，要求无论是输入`任务名称`、`论文题目`、`论文方法`、`论文数据集`，都能得到相应的检索结果，如下例所示：

[![xNHo2q.png](https://s1.ax1x.com/2022/10/11/xNHo2q.png)](https://imgse.com/i/xNHo2q)


+ 可以自己实现搜索算法，也可以使用已有的搜索引擎工具，比如[Elasticsearch](https://www.elastic.co/)

### 展示模块

#### 要求

+ 设计并实现一个论文标签检索引擎网站，包括三个页面：

  + 首页/搜索页

  + 检索结果列表页

    + 上述四项任务分开展示

  + 详情页

    + 需包含上述四项任务详情页，如[任务](https://paperswithcode.com/task/image-classification)，[论文](https://paperswithcode.com/paper/human-motion-diffusion-model)，[方法](https://paperswithcode.com/methods/category/attention-mechanisms)，[数据集](https://paperswithcode.com/dataset/cifar-100)
    + 可选加分项：
      + 根据标签网络计算每个标签的重要性分数并展示
      + 构建在特定任务和数据集下的模型历史发展折线图和排行耪

    ![image-20221012133336146](https://s1.ax1x.com/2022/10/13/xa6sJS.jpg)   

    + 其他有创意的趣味展示

+ 推荐使用 [Python Django](https://www.djangoproject.com/) 库来实现


### 提交内容

+ 一个**MongoDB**数据库
+ 在仓库`README`中给出爬取数据的**统计信息**，例如爬取的论文数、数据集数、字段覆盖率等
+ 验收时，展示论文标签搜索引擎的检索结果



## Project3: 学术类综合检索引擎

### 爬虫模块

+ Paper
  + SciHub：[http://www.sci-hub.ac.cn/](http://www.sci-hub.ac.cn/)
+ e-book
  + library genesis：[http://gen.lib.rus.ec/](http://gen.lib.rus.ec/)
  + eBooks：[http://www.ebooks.com/en-us/free/](http://www.ebooks.com/en-us/free/)
+ PPT
  + PPT Silver：[https://www.slideserve.com/tress/silver](https://www.slideserve.com/tress/silver)
+ Video
  + Bilibili：https://www.bilibili.com/
  + Youtube：https://www.youtube.com/

### 检索模块

#### 要求

+ 从MongoDB中读取数据实现**综合检索**，要求无论是输入`论文`、`电子书`，都能得到相应的检索结果
+ 需要可以查看论文和电子书对应的PPT和视频，设计方法**去杂去重**，保证对齐的准确率

![image-20221013110638629](https://s1.ax1x.com/2022/10/13/xa6yRg.png)


+ 可以自己实现搜索算法，也可以使用已有的搜索引擎工具，比如[Elasticsearch](https://www.elastic.co/)
+ 要求展示模块提供`论文电子书检索列表`、`PPT视频查看按钮`
+ 要求说明筛选PPT和视频的方法原理

### 展示模块

- 设计并实现一个学术类综合搜索引擎网站，包括三个页面

  - 首页/搜索页
  - 检索结果列表页
  + 论文/电子书详情页面：
    + 包含论文标题、作者、摘要等相关信息

- 展示样例如下图所示：
  

[![xNHIGn.png](https://s1.ax1x.com/2022/10/11/xNHIGn.png)](https://imgse.com/i/xNHIGn)

- 推荐使用 [Python Django](https://www.djangoproject.com/) 库来实现

#### 提交内容
+ 一个**MongoDB**数据库
+ 在仓库`README`中给出爬取数据的**统计信息**，例如每个数据源爬取的标签数、字段覆盖率等
+ 展示可视化搜索引擎



# 组队要求

分为12个组，每组5-6人。组内可能会涉及到爬虫、检索、展示等多维度的工作，希望合理分工，紧密配合

- 在**10.15日23:55分**前完成组队，由组长在[腾讯文档](https://docs.qq.com/sheet/DV29HUUxsZmJ2cnhz?tab=BB08J2)中填写队伍信息

- 在**10.16日23:55分**填写志愿，选择想要完成的Project

- 在**10.17日10点**由助教统一抽选，公布选题结果

- 公布每组选题后，每位同学点击以下链接，按照GitHub Classroom引导完成操作：

  - Project1 : https://classroom.github.com/a/yegVQMPh
  - Project2 : https://classroom.github.com/a/GrM0q_9W
  - Project3 : https://classroom.github.com/a/SWE_DDiH

  其中，队长负责创建队伍，其余队员加入已有队伍即可。注意，队名只能是英文名

- 最终所有仓库都会建立在[BITCS-Information-Retrieval-2022-2023](https://github.com/BITCS-Information-Retrieval-2022)这个GitHub Organization账号下

# 验收

| 队伍编号 |   任务   |         组名         |  组长  |                      组员                      | 验收时间    |
| :------: | :------: | :------------------: | :----: | :--------------------------------------------: | ----------- |
|    1     | Project1 |            | 王朝阳 |        汪俊凯，喻晨曦，吕卓澄，崔文耀，林泽炜        | 8:00-8:30  |
|    2     | Project1 |                 |  叶语霄  |  张庚辰，梁瑛平，罗潘亚欣，张驰，魏慧聪  | 8:40-9:10   |
|    9     | Project1 |                 | 于翔 |     赵曰皓，郭思涵，闫羽，彭炜，刘昕飏     | 9:20-9:50   |
|    12     | Project1 |  |  罗泽宇  |       刘奕凡，吕非浓，耿明灏       | 10:00-10:30 |
|    5     | Project2 |                  | 牟效仑 |     方胜，刘彬，刘正清，杨东东，杨芊雨     | 10:40-11:10 |
|    8    | Project2 |             | 任博文 |      王逸洲，缪思语，武益霄，李曼秋，崔文毓      | 11:20-11:50 |
|    10    | Project2 |           | 王恒烨 |      王嘉宁，周旭鸿，邹怡清，李鸿熙，宁艺凯      | 14:00-14:30 |
|    11    | Project2 |                | 邱峙清 |       贾星辰，赵亦锐，刘翔宇，沈洪宇，宫业梓       | 14:40-15:10 |
|    3     | Project3 |                 |  徐正斐  |      米昊天，张成喆，张圃瑒，钱海，杨欣运      | 15:20-15:50 |
|    4     | Project3 |                | 康行铠 |      张敬铮，晁洋，白宇晗，欧立炜，杨崇盛      | 16:00-16:30 |
|    6     | Project3 |                 |  柳思涵  |      刘思雯，贾奥，张蔚，桂梦婷，李翰杰      | 16:40-17:10 |
|    7     | Project3 |                 | 周祐超 | 刘润衡，李云龙，刘进宇，刘冉 | 17:20-17:50 |

+ **时间**：2022/12/18日（周日），上午8:00-12:00，下午14:00-18:00

+ **地点**：中教1003会议室

  + 会议室有投影，需要投影展示，投影仪为HDMI接口，请各组自备**转接头**

+ **验收流程**：

  + 展示时间：15min展示+10min提问
  + 展示内容：包括但不限于整体效果、功能特色、系统架构、代码实现、团队协作情况
  + 展示形式不做限制，以讲清楚作业内容为目的，PPT可根据展示需要选择

+ 文件提交：

  + **代码**部分在验收开始前应当全部上传到小组的GitHub仓库，代码应当结构清晰

    验收时会用Python的[Flake8](https://flake8.pycqa.org/en/latest/)库检查每个小组的代码是否规范，通过检查即可获得代码风格分数，不通过则不会获得

    命令行flake8

    ```
    pip install flake8
    flake8 --max-line-length 127 --ignore=F401,W503 ./
    ```

    vscode配置

    ```
    {
      "python.linting.enabled": true,
      "python.linting.flake8Enabled": true,
      "python.linting.flake8Args": [
          "--max-line-length=127",
          "--ignore=F401, W503"
      ]
    }
    ```

  + **README文件**应该体现出作业要求，此外还要讲述清楚代码目录结构，代码必要说明，部署过程，启动运行流程，依赖的第三方库的目录及版本等，总之，达到路人看到这个文件就能启动这个模块的效果。**该文件将会作为重要评分依据**。
  + **数据部分**应该按照清晰的结构进行存储，验收时拷到助教的移动硬盘中，文件夹中也应当包含一个说明文档
