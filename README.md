# DEPRECATED

# Fast gzip middleware for Gin-Gonic

This gzip middleware uses the `github.com/klauspost/compress/gzip` compression package instead of the standard `compress/gzip`.

### Example Usage:

```go
package main

import (
	"fmt"
	fastGzip "github.com/gagliardetto/gzip"
	stdGzip "github.com/gin-gonic/contrib/gzip"
	"github.com/gin-gonic/gin"
)

var (
	router      *gin.Engine
	testContent []gin.H
)

func init() {
	testContent = []gin.H{
		{
			"abcdefghijklmnopqrstuvwxyz0": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz1": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz2": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz3": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz4": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz5": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz6": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz7": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz8": "12345678910111213141516171819202122232425262728293031323334353637383940",
			"abcdefghijklmnopqrstuvwxyz9": "12345678910111213141516171819202122232425262728293031323334353637383940",
		},
	}

	gin.SetMode(gin.ReleaseMode)
	router = gin.New()
	router.Use(gin.Recovery())
}

func main() {

	router.GET("/fastGZIP", fastGzip.Gzip(fastGzip.DefaultCompression), func(cc *gin.Context) {
		cc.IndentedJSON(200, testContent)
	})

	router.GET("/stdGZIP", stdGzip.Gzip(stdGzip.DefaultCompression), func(cc *gin.Context) {
		cc.IndentedJSON(200, testContent)
	})

	fmt.Println("server started")
	router.Run(":8080")
}

//siege -b -t10S http://127.0.0.1:8080/stdGZIP
//siege -b -t10S http://127.0.0.1:8080/fastGZIP
```

