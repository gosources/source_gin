# 怎么进行开源项目

1. 打开链接: https://github.com/golanglibs/source_gin
2. Fork此项目

![img](./images/merge_request1.png ''图片title'')

![img](./images/merge_request2.png ''图片title'')


![](./images/merge_request3.png)

3. Clone代码并提交
```
$ git clone git@github.com:zhaoweiguo/source_gin.git   // zhaoweiguo改成自己的用户名
$ git remote add upstream git@github.com:golanglibs/source_gin.git   // 设定好源项目的upstream
$ git fetch upstream   // 同步代码
... ...   // 修改代码
$ git add .
$ git commit -m "xxxx"
$ git push origin master
```






