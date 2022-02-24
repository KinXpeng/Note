#### Go 语言

![image-20220113091358643](../../imgs/image-20220113091358643.png)

##### Go入门及基础指令

- 常用指令

  - 运行文件

    ```go
    go run index.go
    ```

  - 编译文件

    ```go
    go build index.go  // 生成一个二进制的可执行文件
    ```

  - 格式化代码

    ```go
    gofmt index.go // 只是将格式化的代码输出
    gofmt -w index.go // 格式化代码并写入文件
    ```

  - 查看数据的类型

    ```go
    var n = 100
    fmt.Printf("n的类型%T",n) // 输出类型
    fmt.Printf("n的类型%c",n) // 格式化输出
    fmt.Printf("n的类型%d",n) // 输出码值
    ```

    

  - 123

- 变量类型及默认值

  - 声明变量

    ```go
    package main
    import  "fmt"
    
    import ( // 引入多个
    	"fmt",
    )
    var ( // 一次性声明， 此处为全局变量
    	m1 = 1
      m2 = 2
      m3 = 3
    )
    func main(){
      var i int
      num := 20 // 可使用 := 赋值，（仅限变量未声明时）
      var n1,n2,n3 int = 1,2,3 // 声明多个变量
      i = 10;
      fmt.Println("i=",i) // 打印
      fmt.Printf("i的类型 %T",i) // 输出数据类型
    }
    ```

  - `int`类型，默认值是0

    ````go
    var i int;
    i = 10
    ````

  - 111

- 123

##### 数据类型

- 基本数据类型

  - 整数的类型

    - int8     有符号  占用1字节  范围（-128～127）
    - int16   有符号  占用2字节  范围（-2^15^～2^15^-1）
    - int32   有符号  占用4字节  范围（-2^31^～2^31^-1）
    - int64   有符号  占用8字节  范围（-2^63^～2^63^-1）

    - unit8   无符号  占用1字节    范围（0～255）
    - unit16 无符号  占用2字节    范围（0～2^16^-1）
    - unit32 无符号  占用4字节    范围（0～2^32^-1）
    - unit64 无符号  占用8字节    范围（0～2^64^-1）
    - int  有符号  32（64）位系统4（8）字节  范围 -2^31^~2^31^-1（-2^63^~2^63^-1）
    - uint  无符号  32（64）位系统4（8）字节  范围 0~2^32^-1（0~2^64^-1）
    - rune  有符号  与int32一样  范围 -2^31^~2^31^-1  等价int32，表示一个Unicode码
    - byte  无符号  与unit8一样  范围 0~255  当要存储字符时选用byte

  - 浮点类型

    - 浮点数都是有符号的
    - `float32`  单精度  `float64` 双精度（推荐使用float64）

  - `string`类型，默认为空字符串

    - go的字符串由字节组成

      ```go
      var a string = "北\n京"  // 双引号会识别转义字符
      var b string = `北\n京`  // 反引号不会识别转义字符，原样输出
      ```

  - 基本数据类型的默认值（go语言中每个数据类型都有一个默认值（也叫零值））

    ```go
    var a int
    var b float32
    fmt.Printf("%v",a)  // %v按照原始值输出
    ```

  - go在不同类型的变量之间赋值时需要显示转换

    ```go
    // 被转换的是变量存储的数据，变量本身的数据类型并没有发生变化。
    var i int32 = 100
    var n1 float32 = float32(i)  // 转换类型
    ```

  - 如果没有用到一个包，可加_忽略

    ```go
    import (
    	_ "fmt" // 忽略此包
    )
    ```

    

  - 1

- 派生/复杂数据类型

#### 包的概念

- 初始化包

  ```go
  // 会在文件目录下创建go.mod文件，引入自定义包是从该目录开始
  go mod init test
  ```

- 1

### 常用方法的封装

- 文件读写

  ```go
  package main
  
  import (
  	"fmt"
  	"os"
  	"bufio"
  	"io"
  )
  
  func main() {
  	srcFile := "./111.txt"
  	dstFile := "./test/222.txt"
  	CopyFile(srcFile, dstFile)
  }
  
  func CopyFile(srcFileName string, dstFileName string) (written int64,err error) {
  	srcFile,err := os.Open(srcFileName)
  	if err != nil {
  		fmt.Println(err)
  	}
  	defer srcFile.Close()
  	reader := bufio.NewReader(srcFile)
  	dstFile,errDst := os.OpenFile(dstFileName, os.O_WRONLY | os.O_CREATE, 0666)
  	if errDst != nil {
  		fmt.Println(errDst)
  		return
  	}
  	defer dstFile.Close()
  	writer := bufio.NewWriter(dstFile)
  	return io.Copy(writer,reader)  
  }
  ```

  

- 2