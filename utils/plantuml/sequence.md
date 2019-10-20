# 目录

- [时序图是什么](#时序图是什么)
- [典型案例](#典型案例)
- [时序图元素](#时序图元素)
- [参考](#参考)

## 时序图是什么

http://plantuml.com/zh/sequence-diagram

时序图sequence diagram也叫序列图、循序图，用于表示类、组件、子系统或参与者的实例之间的消息序列。

## 典型案例

### 微信授权登录👇

![](/imgs/pu-sequence.jpg)

### Plantuml生成的时序图👇

![](/imgs/pu-sequence2.jpg)

### 最简单的时序图

```text
@startuml
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response
@enduml
```

![](/imgs/pu1.jpg)

## 时序图元素

### 1. 对象/角色

对象放置在时序图的顶部，一般是用户、某个系统、某个 服务或者某个数据库

- 如果对象是人，使用actor关键字
- 如果对象是数据库，使用database
- 其他使用participant表示

### 2. 生命线LifeLine

生命线代表时序图中的对象在一段时期内的存在。

时序图中每个对象和底部中心都有一条垂直的虚线，这就是对象的生命线，对象间的消息存在于两条虚线间。

生命线是一个时间线, 从时序图顶部一直到底部都存在, 其长度取决于交互的时间。

### 3. Activation激活

Activation指的是生命线上窄长的矩形条，当对象的生命线出现Activation时代表对象已被激活。

### 4. 消息

表示对象间发送/返回的信息，一般分为以下几种：

- 同步消息Synchronous messages：同步消息是由发送方传递消息后，停止活动，等待接收方返回消息。实线加实心箭头plantuml书写为`->`。
- 异步消息Asynchronous Messages：异步消息不需要等待接受返回信息就进行下一步操作。实线加空箭头plantuml书写为`->>`。
- 返回消息：虚线加箭头plantuml书写为`-->`
- 创建新消息：消息使用`<<>>`括起来
- 自关联消息Self Message：`Alice -> Alice`

### 5. 分隔符「plantuml独有」

分隔符用来分割多个步骤。

![](/imgs/pu-sequence3.jpg)

# 参考

- [geeksforgeeks - Sequence Diagrams](https://www.geeksforgeeks.org/unified-modeling-language-uml-sequence-diagrams/)
- [csdn - UML时序图](https://blog.csdn.net/fly_zxy/article/details/80911942)