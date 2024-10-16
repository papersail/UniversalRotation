原贴地址：https://www.jisilu.cn/question/457389

下载源码的方式：点击GitHub网页上的Code按钮，选择自己喜欢的下载方式即可：
![](res/download.png)

### 联系作者
如果想讨论该tool的用法或者新需求，以及量化轮动策略等相关的内容，可以关注公众号“多策略再平衡小杠杆对冲”(wangbaobaoyzy)，共同学习和进步！

![](res/author.png)

### 使用前准备
1. 安装Python3：https://www.python.org/ftp/python/3.8.7/python-3.8.7-amd64.exe
2. 打开cmd窗口输入：pip install schedule xlwings pandas requests pysnowball browser-cookie3 chinese_calendar
3. 启用Microsoft Office（不要使用WPS）的Excel中的xlwings宏：
   (1)、命令行安装加载项：xlwings addin install。
   (2)、在excel中启用加载项： 文件>选项>信任中心>信任中心设置>宏设置 中，选择“启用所有并勾选”并勾选“对VBA对象模型的信任访问”。 
4. 设置Firefox(强烈推荐)或Chrome(我用的版本是108.0.5359.125，建议使用最新版，因为太多网友因为版本太低导致无法使用browser-cookie3)或Opera或Edge或Chromium为默认浏览器，使用他们的任意一个访问任意一个雪球网站以便获取token（不需要登录雪球账号）。

注1：如遇到如下报错就代表token过期了：
Exception: b'{"error_description":"\xe9\x81\x87","error_uri":"/v5/stock/quote.json","error_data":null,"error_code":"400016"}'。
由于我们在Python调用雪球API前需要设置xq_a_token，但它大约只有20天的有效期，之前都是使用F12各种查找xq_a_token然后复制粘贴到我们的Python程序，
比较繁琐，所以现在改用browser-cookie3工具库来自动化获取电脑浏览器已缓存的cookies（当然啦，浏览器的cookies肯定也会过期，我们只需要坚持每20天左右使用电脑浏览器访问任意一个雪球网站即可刷新电脑浏览器的cookies）。
但是我发现网友经常遇到Chrome浏览器无法使用browser-cookie3的问题，是因为Chrome浏览器的版本太低导致的。所以建议大家使用Firefox为默认浏览器或者更新到最新版Chrome浏览器。

注2：如遇到如下报错就代表chinese_calendar过期了：
no available data for year 2023, only year between [2004, 2022] supported.
需要升级：pip install -U chinesecalendar

注3：作为一个Android程序员，从2022.2月份开始边学边练第一次写Python项目进行量化投资，语法格式肯定不完美，勿喷，仅仅是为了解放调仓的苦恼而写的小玩意，分享出来仅用于学习研究，不可用于商业用途！

### (一)、使用Python+Excel可视化你的持仓和最新排名的差异，解决买什么卖什么的烦恼
1. 这里以"低溢价可转债策略"( https://xueqiu.com/P/ZH3128720 )、"双低可转债策略"( https://xueqiu.com/P/ZH2982722 )为例子，我做了2个轮动的sheet表格：《低溢价可转债轮动》和《双低可转债轮动》。 
2. 点击《可转债实时数据》里面的“点击更新”按钮。 
3. 分别点击《低溢价可转债轮动》和《双低可转债轮动》里面的“点击更新”按钮，如果有其他任何自定义排名也可以手动更新”最新多因子1/2可转债排名“。
4. 从券商PC端软件导出最新的低溢价可转债持仓和双低可转债持仓的Excel表格，并分别更新到“我的低溢价可转债持仓”、“我的双低可转债持仓”，这时候就可以看到需要轮动的结果了。

注3：这里依赖的是Excel自带的各种公式，忽然发现Excel解放手脚的强大了吧？神不神奇惊不惊喜，意不意外?

注4：每个sheet页我都做了双排名（即自定义的”最新多因子1/2可转债排名“），满足用户自定义的需求。

注5：这里的2个sheet页仅是2个可转债的例子，填充了持仓和最新排名。用户可以将它应用于任何的“依据各种因子进行排名的量化轮动策略”。
大家可以将这两个sheet作为壳子，替换成任何你们自己的轮动品种，比如小市值低价股票策略、低估股票策略、A/H轮动等等。


### (二)、关于《20天净值增长率和溢价率轮动LOF、ETF和封基》和《20天净值增长率和溢价率轮动债券和境外基金》
1. 点击“点击更新”按钮，即可更新这2个策略(https://xueqiu.com/P/ZH3040077 和 https://xueqiu.com/P/ZH3044957 )的最新的排名数据。
2. 从券商PC端软件导出我的持仓放在左侧列表，即可看到目前持仓排名了。