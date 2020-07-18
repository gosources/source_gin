## 重要源码

- 核心代码:
    - gin.go
    - routegroup.go
    - context.go
    - response_writer.go
- 底层代码:
    - tree.go
- 中间件:
    - logger.go
    - recovery.go
- debug专用:
    - mode.go
    - debug.go
- 工具代码:
    - utils.go
    - path.go
    - errors.go
- 边角:
    - fs.go
    - auth.go
- render目录
- binding目录


## 疑问

1.这句语法的含义是什么？只是证明这个类实现了这个Interface？
```
var _ StructValidator = &defaultValidator{}
```
2. [...]是什么意思？
```
routes := [...]string{
  "/hi",
  "/contact",
  "/co",
  "/c",
  "/a",
  "/ab",
  "/doc/",
  "/doc/go_faq.html",
  "/doc/go1.html",
  "/α",
  "/β",
}
```

## 主要函数分拆

#### func (n *node) insertChild:

```
1. 参数相关处理:
    beginning with ':' or '*'
    @todo
2. 赋值node:
  n.path = path[offset:]
  n.handlers = handlers
  n.fullPath = fullPath
```
#### func (n *node) addRoute
```
1. 是否空树判断
2. 非空树
    for循环执行相关操作
    @todo
3. 空树:
    n.insertChild(numParams, path, fullPath, handlers)
  n.nType = root  // root=1
```

#### func (n *node) getValue
```
1. 返回值nodeValue类型格式:
    type nodeValue struct {
      handlers HandlersChain
      params   Params
      tsr      bool
      fullPath string
    }
2. if len(path) > len(n.path) 且 前面部分相同
    2.1 wildChild相关处理 @todo
    2.2 验证children的nType==param
    @todo
    2.3 验证children的nType==catchAll
    @todo
3. if len(path) == len(n.path)
    3.1 n.handlers != nil:
        value.handlers = n.handlers
        value.fullPath = n.fullPath
    return
  3.2 其他情况处理
  @todo
```

#### func (engine *Engine) handleHTTPRequest
```
1. 对UseRawPath的处理
@todo
2. cleanPath函数功能
@todo
3. 主处理逻辑
    3.1 获取root trees(即get, post...每个一个root), for循环验证每一个类型
    3.2 httpMethod不同的直接不匹配，继续下一个
    3.3 调用root.getValue函数获取此tree下nodeValue格式的数据
    3.4 value.handlers不为nil时:
        c.handlers = value.handlers
    c.Params = value.params
    c.fullPath = value.fullPath
    c.Next()    // 分别执行所有的handlers(包括r.GET等&中间件engine.Use(xxx))
    c.writermem.WriteHeaderNow()
    return
  3.5 value.handlers等于nil时:
      应该是跳转处理
      @todo
4. HandleMethodNotAllowed相关处理
@todo
5. 最后没有相关路由的处理
@todo
```



