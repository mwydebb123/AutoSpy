# auto_spy

## 介绍
简单介绍一下SPY的功能：
**监听**（跟傻妞的SPY一样）：自动监听设置好的频道或群，捕捉关键词，并转换成你脚本对应的环境变量，自动启动对应的任务

**队列**：当瞬间涌入多个同一脚本变量时，自动进入队列，当前面一个跑完，根据设置延时，自动跑下一个变量，有限抢占最新变量，并且不会遗漏线报做到捡漏；

**多频道**：每个频道线报优势均有所不同，SPY支持多频道监听，不同变量自动转换成脚本对应环境变量，实现多频道自动监听；

**去重**：多个频道线报有先后，内容有重复，SPY自动去重，防止跑无用线报内容，抢占第一手脚本运行；

**多任务**：每个脚本对应一个任务，均采用多线程管理，独立运行，互不干扰；

**不易黑IP**：因为是队列，每次跑的间隔自行设置，所以只要调整得当，不易黑IP，当然脚本造成的黑没有办法；



## 安装教程

1.  准备好docker环境；

2.  进入终端，在你想要存储SPY信息的文件夹下运行一键安装，仅需打开一次，然后执行强制升级
   ```
   wget -O autospy https://github.com/xieshang/AutoSpy/raw/master/docker.sh && chmod +x autospy && ./autospy
   ```
   强制升级：
   ```
      cd auto_spy_data/autospy && bash <(curl -s -L https://github.com/xieshang/AutoSpy/raw/master/spy_update.sh)
   ```
   
   第一次运行完成后，按提示修改配置文件，特别是TG和青龙的配置

3. 修改完配置后，再次运行一键脚本，记住，要回到你刚才的目录下运行，否则又会建一个SPY的配置文件。
   
4. 提示输入电话号码的时候，请在前面加上"+86"，如果不是中国的手机，那么就别用SPY了，没意思。
   TG的登录过程与人形一致，可以参考一些人形教程


## 配置文件修改

1.  配置文件<auto_spy.yaml>内容
   ````
# 授权信息  在群内发送 "/SPY 授权"  机器人将自动私发给你
Aauthentication: 111112222333sdfafdsf
# 青龙相关信息
QingLong:
  # 只需提供任务权限即可
  # 青龙id
  Client_ID: asdfsdff
  # 青龙secret
  Client_Secret: safsdfsaf
  # 多容器选择切换间隔
  Container_Wait: 3
  # 任务结束后等待多久再次执行
  WaitTime: 10
  # 青龙url
  url: http://192.168.1.250:5700

# TG信息
Telegram:
  # TG api hash
  api_hash: api_hash
  # TG api id
  api_id: api_id
  # 监听频道、群id
  listen_CH:
  - -10016
  # 你的日志输出群ID(有人形傻妞)，或者傻妞机器人ID
  log_id: -1001
  # 管理员id
  master_id:
  - 188111
  # socket5代理IP，国内机必须填写，否则不能登录
  proxy_ip: ''
  # 代理port
  proxy_port: 11223

# 脚本配置
js_config:

# CJ组队任务
- Container:
  # 傻妞多容器配置，当需要第1个容器运行时，填1，全部配置填a，若分别多个容器，可填[1,3]，一个容器就留空
  - []
  # 要设置的环境变量名称，配合脚本使用
  Env: jd_cjzd
  # 要监听的变量参数，可配合Env实现环境变量的转换，因为不同频道的变量都有可能不同
  KeyWord:
  - - 频道1变量A1
  - - 频道2变量A2
  # 任务名字
  Name: cj组队
  # 青龙脚本的关键词，必须为唯一搜索到的关键词，否则将自动取第一个脚本作为运行
  Script: jd_team60.js
  # 脚本运行超时时间，暂不支持
  TimeOut: 0
  # 配置完环境变量等待多久再运行脚本
  Wait: 3

   ````

#### SPY指令
1、**spy**：查看队列情况，10秒后自动撤回；
2、**spy 重启**：重启SPY；
3、**spy 升级**：升级到最新的SPY；


#### 问题排查
* 登录TG的时候没跳出来要求输入电话？
```
    请确认配置文件的API和hash是否填写正确；
```

* SPY是否已经成功启动？
```
在命令行输入： docker logs auto_spy

查看日志是否报错
如果日志看不懂，可以先复制一下，到百度翻译一下再提问
```

* 群内可以看到自己鉴权并且很快撤回，说明已经成功，但是发送spy没反应？
```
请确认是设置错了管理员id？
```

* 脚本怎么配置？
```
别问我，偷撸脚本自己找，公开的脚本去对应频道看看也都知道怎么写了。
```