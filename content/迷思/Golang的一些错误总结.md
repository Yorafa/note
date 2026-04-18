### Go mod 相关

go get
go install
require, exclude, replace, retract
go mod

### Go Test 相关

#### Go Test:

测试文件一般与源文件放在一起，测试文件名字一般为 `源文件_test.go`.

- Unit test 主要依赖 `testing` module, 对于测试的 function 需要添加参数`(t *testing.T)`
- 在一个function中可以进行多个测试，只需使用`t.Run(name, testFunc)`
- 在需要 helper function 时， 需要手动在helper function里添加 `t.Helper()`

Go mock

### String 相关

### 类型转换类错误

在写`IntHeap`的时候对已有的`[]int`进行类型转换不能直接引用, 例如:

```go
type IntHeap []int

/*
	Implement of heap interface method
*/

func main() {
	nums := []int{1,2,3,4,5,6}
	h := IntHeap(nums) // fine
	h := &IntHeap(nums) // compiler error
}
```

这是因为直接 `&IntHeap(nums)` 也就是直接引用临时变量的地址是不可取的 ( go的语法规范 )。但这样的语法规范刻意保证变量是安全的
