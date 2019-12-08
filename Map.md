# Map

##  创建

make(map[string]int)

## 获取元素

m[key]

当key不存在的时候，获得value类型的初始值

用value,ok := m[key]来判断是否存在key

## 遍历

使用range遍历key,或者遍历key,value对

不保证顺序，如需顺序，需手动对key排序

使用 `len` 获取元素的个数



## map的key

map使用哈希表，必须可以比较相等

除了slice，map，function的内建类型都可以作为key

Struct 类型不包含上述字段，也可以作为key，会自动检查是否含有非法内建类型

```go
func main() {
	m := map[string]string {
		"name": "ccmouse",
		"course": "golang",
		"site":"imooc",
		"quality":"notbad",
	}

	m2 := make(map[string]int) // m2 == empty map

	var m3 map[string]int // m3 == nil

	fmt.Println(m, m2, m3)

	for _, v := range m  {
		fmt.Println(v)
	}

	// 多次遍历的顺序可能不同，无序
	for k, v := range m  {
		fmt.Println(k, v)
	}

	fmt.Println("Getting values")
	courseName, ok := m["course"]
	fmt.Println(courseName, ok)

	// 取出不存在的key时，也能获取到值，这个值是一个空字符串
	if causeName, ok  := m["cause"]; ok {
		fmt.Println(causeName)
	} else {
		fmt.Println("key does not exists")
	}

	fmt.Println("Deleting values")
	name, ok := m["name"]
	fmt.Println(name, ok)

	delete(m, "name")
	name, ok = m["name"]
	fmt.Println(name, ok)
}
```

