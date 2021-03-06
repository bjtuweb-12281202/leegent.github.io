# 任务二十八：行星与飞船（三）

**面向人群：**
有一定JavaScript基础，希望学习或加强面向对象编程及设计模式相关知识的同学

**难度：**
中等

## 任务目的
- 练习JavaScript面向对象设计
- 实践一些基础的设计模式

## 程序说明

- 整个程序分为控制台、媒介（BUS）、行星、飞船四大模块，其中行星上又有指挥官、飞船工厂、信号接收器和数据中心四个子模块
- 控制台：持有游戏界面的控制台。这个模块比较特殊，因为需要输出信息的地方比较多，所以调用控制台的语句到处散落，但逻辑上并没有什么耦合，删去不影响主体功能
- BUS：中介者，行星与飞船之间的一切联系都需要通过BUS，也是飞船发射后唯一直接打交道的模块
- 行星：一个复杂的模块，其内部的四个子模块关系相对紧密：
    - 1.指挥官：持有游戏界面上的命令面板，具备向BUS发射指令的功能，也可以命令飞船工厂发射飞船
    - 2.飞船工厂：负责发射飞船，管理飞船id；可以向指挥官反馈飞船发射成功，使其添加飞船的命令面板；也可以向数据中心通告飞船发射成功，令其在监控界面添加新飞船
    - 3.信号接收器：功能很单一，接收BUS发来的信息并转交给信息中心。我给它附加了过滤命令广播的功能。它存在的意义是在BUS里为行星提供一个观察者接口。
    - 4.数据中心：持有游戏界面上的显示屏，可以解码由信号接收器转交的飞船状态广播并显示出来。当收到飞船“待销毁”的状态广播时，通知飞船工厂将飞船的id重新设为可用。
- 飞船：飞船的构造函数比较大，放在一个单独的文件spacecraft.js里
    - 飞船内部有三个主要的系统：能源，动力，控制。前两个系统互不访问，由控制系统集中管理。另外有一个信号发射器，不断向BUS广播自身状态
    - 控制系统向上承接指令，向下指挥其他系统执行指令。自毁功能也在控制系统内
    - 内部变量和函数用下划线表示，建议不直接访问（本来打算用闭包封装，但这样无法使用原型继承，对内存开销有影响）
    - 飞船暴露给外界的接口有3个：getId(),getSystemType()和onReceiveMessage()
    - 飞船的初始化参数一概由飞船工厂提供，各处注册也基本由工厂负责，除了BUS那里（可以这样理解，飞船一诞生就自动存在于介质中，销毁时也自动从BUS消失，并不是通过工厂代劳）

- 想请教在设计模式、编码风格等等各方面还有哪些可以改进的地方？以及下一步建议的学习方向？谢谢！

