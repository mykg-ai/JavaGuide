# 目录

- []()
- [参考资料]()

crond
- https://www.cnblogs.com/ftl1012/p/crontab.html
```
 -u <user>  define user
 -e         edit user's crontab
 -l         list user's crontab
 -r         delete user's crontab
 -i         prompt before deleting
 -n <host>  set host in cluster to run users' crontabs
 -c         get host in cluster to run users' crontabs
 -s         selinux context
 -x <mask>  enable debugging
```
```
service crond status

crontab -l

crontab -e

0 3 * * * sh /data/gitlab/backup.sh
```

## 参考资料

- [cnblog - 小a玖拾柒 - Linux crontab命令详解](https://www.cnblogs.com/ftl1012/p/crontab.html)