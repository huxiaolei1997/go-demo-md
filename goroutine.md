# goroutine

协程 Coroutine

轻量级 `线程`

`非抢占式`多任务处理，由`协程`主动交出控制权，不是由操作系统决定的，消耗资源较少，编译器/解释器/虚拟机层面的多任务，操作系统中没有协程

`多个协程`可能在`一个或多个线程`上运行



子程序是协程的一个特例



`线程`是抢占式的，控制权在操作系统，可能任务没有执行完毕，就

会被操作系统中断，让出CPU时间片给其它线程执行任务

![image-20191222181701048](https://tva1.sinaimg.cn/large/006tNbRwgy1ga5o333p7vj31cm0qual0.jpg)



其它语言中的协程

Python 3.5 加入了 aysnc def 对协程原生支持

C++

Java原生不支持，有些第三方的JVM支持协程



![image-20191222181911409](https://tva1.sinaimg.cn/large/006tNbRwgy1ga5o5cbn9cj31cu0pwqes.jpg)



任何函数只需加上`go`就能送给调度器运行

不需要在定义时区分是否是异步函数

调度器在合适的点进行切换，不用手动去切换

使用 -race 来检测数据访问冲突

goroutine可能切换的点

I/O，select

channel

等待锁

函数调用

runtime.Gosched()

![image-20191222182154193](https://tva1.sinaimg.cn/large/006tNbRwgy1ga5o84sx68j31960nw10o.jpg)





```go
package main

import (
	"fmt"
	"time"
)

//import "golang.org/x/tools/go/ssa/interp/testdata/src/fmt"

func worker(id int, c chan int) {
	for n := range c {
		// 从channel中取出数据
		//n := <- c
		//n, ok := <- c
		//
		//if !ok {
		//	break
		//}

		fmt.Printf("Worker %d received %c\n", id, n)
	}
}

// 创建一个只能收数据的channel
func createWorker(id int) chan<- int {
	c := make(chan int)
	go worker(id, c)
	return c
}

func chanDemo() {
	//var c chan int // c == nil
	var channels [10]chan<- int
	for i := 0; i < 10 ;i++  {
		channels[i] = createWorker(i)
	}

	// 向channel中发送数据
	for i := 0; i < 10; i++  {
		channels[i] <- 'a' + i
	}

	time.Sleep(time.Millisecond)
}

func bufferedChannle() {
	c := make(chan int, 3)
	go worker(0, c)
	// 发数据必须要有程序来接收
	c <- 'a'
	c <- 'b'
	c <- 'c'
	time.Sleep(time.Millisecond)
	//c <- 4
}

func channelClose()  {
	c := make(chan int)
	go worker(0, c)
	// 发数据必须要有程序来接收
	c <- 'a'
	c <- 'b'
	c <- 'c'
	// 发送方close
	close(c)
	time.Sleep(time.Millisecond)
}
func main() {
	//chanDemo()
	//bufferedChannle()
	channelClose()
	// go语言并发基于CSP模型
}
```



![image-20191222191926692](https://tva1.sinaimg.cn/large/006tNbRwgy1ga5pw2g281j315m0i8wjd.jpg)