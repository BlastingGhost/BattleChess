# BattleChess

## 0. 前言

QQ宠物里面有一个游戏叫做皇家战棋，我女朋友很喜欢玩，但是腾讯前不久关闭了QQ宠物，这个游戏也没地方玩了。所以我就准备自己写一个，刚好最近也租了一个云服务器，可以尝试写一个可以联网对战的。

游戏用到的素材都是网上找的图片，然后再自己去抠图加工，棋子是在一个素材网站下载的。

开发环境是：

- windows 10

- python 3.5+
- pygame >= 1.9.5
- twisted >= 19.7.0

在Linux下运行会出现中文字体无法显示的问题，还待解决。

本项目地址：[BattleChess](https://github.com/MemoryD/BattleChess/)

## 1. 游戏说明

### 1.1 等级划分

每一方的有 18 个棋子，具体如下：

- 刺　客：一星 ★　共 8 个
- 禁卫军：二星 ★★　共 4 个
- 弓箭手：三星 ★★★　共 2 个
- 骑　士：四星 ★★★★　共 2 个
- 将　军：五星 ★★★★★　共 1 个
- 国　王：六星 ★★★★★★　共 1 个

当轮到一方行动时，可以用自己的棋子吃掉对方等级小于或等于己方棋子等级的棋子。但是刺客可以吃掉国王，而国王不能吃掉刺客。具体可以看下图：

![等级说明](https://raw.githubusercontent.com/MemoryD/BattleChess/master/screenshot/level.jpg)

### 1.2 输赢条件

以下是游戏的输赢条件，没打勾的是还没实现的功能。

- [x] 一方吃掉对方全部棋子时获胜。 
- [x] 当双方各剩下一颗棋子时比较大小，棋子大的一方获胜；但如果剩下国王和刺客，刺客方获胜。 
- [x] 在20秒内没有走步计超时一次，累积超时3次会被判输。
- [x] 一方可以提出认输，开局后20步之内不可以提出认输。
- [x] 一局游戏中连续30步没有吃子或翻牌则自动算和棋。 
- [ ] 一方可以提出求和，对方同意后按和棋处理。



### 1.3 积分系统

根据用户积分的不同，会有不同的称号，如下：

|   积分   |   称号   |
| :------: | :------: |
|   < 40   |   平民   |
|  < 100   | 小农场主 |
|  < 200   | 大农场主 |
|  < 360   |   贵族   |
|  < 760   |  小城主  |
|  < 1400  |  大城主  |
|  < 2600  |   男爵   |
|  < 4400  |   子爵   |
|  < 7600  |   伯爵   |
| < 15000  |   侯爵   |
| < 33000  |   公爵   |
| < 65000  |   国王   |
| >= 65000 |   教皇   |

积分的计算规则如下：

- [x] 赢一场比赛（包括对方认输，掉线），积分 +20。
- [x] 输一场比赛（包括认输），积分 -20。
- [x] 双方和棋，积分均不变。
- [x] 因为掉线而输掉比赛，目前不扣分（后续可能会改进）。

---

## 2. 运行截图

- 登录：

  ![等级说明](https://raw.githubusercontent.com/MemoryD/BattleChess/master/screenshot/login.png)

- 开始界面：

  ![等级说明](https://raw.githubusercontent.com/MemoryD/BattleChess/master/screenshot/begin.png)

- 游戏界面：

  ![等级说明](https://raw.githubusercontent.com/MemoryD/BattleChess/master/screenshot/local.png)



---

## 3. 运行说明

### 3.1 直接运行

如果你想要直接在Windows上运行，那你可以下载 [releases](https://github.com/MemoryD/BattleChess/releases) 中的 `windows-battlechess-vx.x.x.zip` ，解压后运行其中的 `battlechess.exe` 就可以了。

### 3.2 使用python运行

#### 方法一：

直接使用 pip 安装：

```sh
pip install battlechess
```

最后在命令行中用如下命令启动游戏：

```sh
python -m battlechess
```

#### 方法二：

下载 [releases](https://github.com/MemoryD/BattleChess/releases) 中的 `battlechess-vx.x.x-py3-none-any.whl` ，然后使用如下命令安装：

```sh
pip install battlechess-vx.x.x-py3-none-any.whl
```

最后在命令行中用如下命令启动游戏：

```sh
python -m battlechess
```

#### 方法三：

将本项目的代码克隆到本地，然后进入文件夹 `BattleChess`，先使用 `pip` 安装依赖：

```sh
pip install -r requirements.txt
```

然后运行游戏：

```sh
python -m battlechess
```



---

## 4. 开发日志

### v1.0.1

时间：2019/11/22  21:45

更新了数据解析的方式，存储服务器数据的地方从一个变量换成一个列表，防止来不及处理。

改变了发给QQ的日志的格式。

### v1.0.0

#### 更新内容

此版本是初始版本，大概完成了大致游戏的编码，但是存在很多Bug，很多功能只是简单实现了一下，毫无安全性和效率可言。

#### 待实现的功能

- [ ] 实现棋盘格子提示颜色的半透明化，让画面更加好看。
- [x] 优化服务端和客户端对网络数据的解析问题，即优化协议。
- [ ] 加入声音。
- [ ] 加入求和模式。
- [ ] 对传输进行加密。
- [ ] 将更多运算放到服务器端。
- [ ] 不发送完整的棋盘，改成每次翻开棋子时再从服务端获取。
- [ ] 校准对战双方的时间差。
- [ ] 将密码改成非明文存储。
- [ ] 优化游戏的性能。

#### 问题记录

- [x] 实现棋盘的 2.5D 效果。

  使用PS做棋盘时发现是是通过投影变换实现的，于是先手动得到变换后的棋盘的四个角点，再结合原本规则的棋盘，通过使用 `opencv` 中的函数 `getPerspectiveTransform()` 来计算投影变换矩阵。然后就可以计算出变换后的棋盘每一个交点的坐标。

- [x] 多线程出错解决。

  因为 `twisted`，`pygame`，`tkinter` 都需要运行在一个死循环中，一般的做法是使用多线程来解决。但是这个库在多线程下都会出现一些问题，比如无法在一个线程启动而在另一个线程结束。

  因此想办法让他们都运行在主线程里，最后采取了 `twisted` 中的 `tksupport` 解决了 `tkinter` 的问题，并且查看了其代码后发现是通过定时的调用 `tkinter` 主控件的 `update()` 方法代替了 `mainloop()` ，因此不会陷入死循环。因此我仿照此想法，定时调用自己游戏的 `run()` 方法，就解决了这个问题。 

- [x] twisted 粘包解决。

  `twisted` 在传输数据的时候会发生这么一种现象，就是客户端分几次发出去的包，在服务端是一次性收到的，因此在服务端需要先把不同的数据包分出来再进行处理。