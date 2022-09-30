

go test简明教程

测试的目的通常是暴露我们更改代码时发生的某种错误。在本文中，我们会就以下几部分内容对Golang测试讲解

* 如何对一个函数或方法进行测试
* Testing.m Testing.t Testing.b的使用与区别
* 高级测试(Mock测试与Monkey打桩测试)

  ---

  常见需求
* flag在Testing.m中的使用
* 如何不测试某一文件
* 如何不测试某一文件夹

  单元测试

  首先 我们的文件名必须以_test.go结尾的，这样在执行go test的时候才会执行到相应的代码

**flag在Testing.m中的使用**

在上面连接中介绍过，TestMain是负责抽象公共逻辑(即test文件会先执行TestMain的逻辑)，那么解析从外部传入的flag也应该放在这一部分做。

```
var systemTestPort = flag.Int("SystemTestPort", 0, "test server run port")
var Port string

func TestMain(m *testing.M) {
   if !flag.Parsed() {
      flag.Parse()
   }
   Port = strconv.Itoa(*systemTestPort)
   setup()
   log.Println("start test")
   exitVal := m.Run()
   log.Println("end test")
   os.Exit(exitVal)
}
```

**如何不测试某一文件**

我们可以使用testing.short()这一变量进行控制。在命令行输入go test -short testfile时，该变量会设置为true，因此可以在test中加入判断。

```
func TestAdd(t *testing.T) {
   if testing.Short() {
      log.Println("skip this test")
      return
}
}
```


**如何不测试某几个文件夹**

可以使用(go list ./... | grep -v filepath)
