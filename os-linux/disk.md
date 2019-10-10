# 目录

- [linux磁盘扩容&分区]()
- [参考资料]()

## linux磁盘扩容&分区

### 1.首先需要查看磁盘的情况

```shell
# 查看分区的名称、容量、已用及磁盘挂载点
$ df -lh
# 比上面的多了文件系统的格式
$ df -Th

# 查看所有物理磁盘及其分区状况
$ fdisk -l

# 以列表形式查看物理磁盘的信息
$ lsblk
```

### 2. 操作分区

看到所有分区后，可以进入任意一块。注意这里也可以直接进入物理磁盘。

如果是扩大分区容量，那么就在这里删除旧的分区，然后创建一块新的代替它，然后跳到3.2来使配置的容量生效。<br/>如果是创建新分区，那就跳到3.1，指定它的文件系统。

这里可以明显看出来vda是一个物理磁盘，而vda1是它的第一个分区。

```shell
# 进入物理磁盘
$ fdisk -u /dev/vda
# 进入分区
$ fdisk -u /dev/vda1

# 查看所有操作命令
$ m

# 查看当前选中的磁盘/分区的分区状况
$ p

# 创建新磁盘，然后选择该分区占用的扇区
$ n

# 删除分区
$ d

# 保存配置并退出
$ w
# 不保存退出
$ q
```

分好区后告诉系统分好了，快生效
```
$ partprobe
```

### 3.1 为新分区分配文件格式
```shell
# 创建ext4文件系统(推荐)：
$ mkfs.ext4 /dev/vdb2
# 创建ext3文件系统：
$ mkfs.ext3 /dev/vdb2
# 创建xfs文件系统：
$ mkfs.xfs -f /dev/vdb2
# 创建btrfs文件系统：
$ mkfs.btrfs /dev/vdb2
```

### 3.2 为旧分区扩容

- resize2fs 针对文件系统ext2 ext3 ext4
```
resize2fs /dev/vdb2
```
- xfs_growfs 针对文件系统xfs
```
xfs_growfs /dev/vdb2
```


```shell
$ df -lh

$ fdisk -l

$ fdisk -u /dev/vda

# 分好区后执行告诉系统分好了
$ partprobe

mount /dev/vda /

umount /dev/vda

df -Th


resize2fs 针对文件系统ext2 ext3 ext4
xfs_growfs 针对文件系统xfs
```

## 参考资料
- https://www.cnblogs.com/youbiyoufang/p/7607174.html
- https://help.aliyun.com/document_detail/25452.html?spm=a2c4g.11186623.2.25.42d64656JtI9lj#concept-z11-xsh-ydb