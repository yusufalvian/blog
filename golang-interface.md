interface adalah blueprint. ia mendefinisikan struktur, tanpa implementasi. contoh interface 
```go
type TheString interface {
	String() string
}
```

suatu type dikatakan telah mengimplementasikan suatu interface jika type tersebut memiliki method yang sama dan return data type yang sama dengan yang dimiliki interface tsb. 
```go
type Book struct {
	Title string
	Author string
}

func (b *Book) String() string {
	return fmt.Sprintf("Book: %s - %s", b.Title, b.Author)
}
```

jika ada suatu function dimana input parameter-nya adalah interface TheString maka semua object yang implement interface tsb bisa digunakan sebagai input parameter-nya. contoh 
```go
func Example(s TheString){
	log.Println(s.String())
}
```

pada contoh di atas, input parameter function Example adalah interface TheString. Object dengan type Book bisa digunakan sebagai input parameter pada function Example karena type Book implement interface TheString 

### empty interface 

empty interface adalah interface yang tidak memiliki method. hal ini berarti semua type bisa implement interface ini. interface ini bisa digunakan jika kita ingin menulis code yang tidak strict type-nya di golang. contoh 
```go
package main

import "fmt"

func main() {
	person := make(map[string]interface{})
	person["name"] = "John Doe"
	person["age"] = 30
	person["weight"] = 50.3
	fmt.Printf("%v", person)
}

```

string, int, dan float bisa digunakan sebagai value karena semua type bisa implement interface{}. namun, kita harus hati-hati dengan implementasi di atas, ketika get value-nya harus di-assert ke value yang diharapkan. ketika ingin akses value dengan key "get" : 
```go
data, ok := person["age"].(int)
if !ok {
	fmt.Println("age is not an int")
}
fmt.Println(data)
```

