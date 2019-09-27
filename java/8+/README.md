Java8，又称jdk1.8，是由Oracle公司于2014年发布，是Java语言开发的主要版本。

# 目录

- [1. Lambda](#1-Lambda)
- [2. 方法引用](#2-方法引用)

## 1. Lambda

Lambda表达式，又称闭包，和js中的箭头函数以及python中的lambda表达式类似，目的是快速创建一个匿名函数并且可以使代码变得更加简洁紧凑。

### 1.1 对列表进行迭代

```
List<String> l = Arrays.asList("a", "c", "b");
l.forEach(c -> System.out.println(c));
```

### 1.2 替换匿名内部类

```

```

### 1.3


## 2. 方法引用

方法引用就是

```
List<String> l = Arrays.asList("a", "c", "b");
l.forEach(System.out::println);
```