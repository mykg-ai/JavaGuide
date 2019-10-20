# 目录

- [类图是什么](#类图是什么)
- [面向对象是什么](#面向对象是什么)
- [典型案例](#典型案例)
- [类图的元素]()
- [参考](#参考)

## 类图是什么

http://plantuml.com/zh/class-diagram

类图(Class diagram)是显示了模型的静态结构，特别是模型中存在的类、类的内部结构以及它们与其他类的关系等。

类图是面向对象建模的主要组成部分。它既用于应用程序的系统分类的一般概念建模，也用于详细建模，将模型转换成编程代码。类图也可用于数据建模。

## 面向对象是什么

面向对象(Object Oriented,OO)是软件开发的一种方法。

## 典型案例

![](/imgs/pu-class1.jpg)

## 类图(面向对象)的元素

### 1. 类 Class

具有相同特征和行为的对象的抽象就是类。

类具有属性。

类具有行为。

```text
@startuml

class Student {
  - String name
  + void goToSchool()
}

@enduml
```

### 2. 接口 Interface

这里的接口和我们通常理解的API接口不同，它是相对于class而言。一般class要明确方法(即行为)的细节，而interface不需要定义出方法内具体的实现，只需要定义有这个方法就可以了。接口需要具象化的类来实现，如创建动物的接口，需要动物的class或者猫的class来实现。

```text
@startuml

interface Student {
  - String name
  + void goToSchool()
}

@enduml
```

### 3. 包 Package

将多个类和接口聚合为一个包。

```text
@startuml

package school {
  interface Student {
    - String name
    + void goToSchool()
  }
}

@enduml
```

### 4. 关系

- extension，父类`<|--`子类
- composition，描述几对几的关系`*--`，如`class1 "1" *-- "n" class2`

# 参考

- [百度百科 - 类图](https://baike.baidu.com/item/%E7%B1%BB%E5%9B%BE/4670826?fr=aladdin)