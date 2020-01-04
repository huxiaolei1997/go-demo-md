# HTTP以及其它标准库



go tool pprof http://localhost:8888/debug/pprof/profile

获取30s内CPU使用率，这时候可以通过频繁访问一个URL来查看这一段时间内CPU使用率

go tool pprof http://localhost:8888/debug/pprof/heap

查看30s内内存使用情况

![image-20200104140306250](https://tva1.sinaimg.cn/large/006tNbRwgy1gakht1939lj30xu0k0dlv.jpg)



## bufio

## log

## encoding/json

## regexp

## time

## strings/math/rand

godoc -http :8888 端口可以自己指定

查看标准库文档

