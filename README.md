# Fast gzip middleware for Gin-Gonic

This gzip middleware uses the `github.com/klauspost/compress/gzip` compression package instead of the standard `compress/gzip`.

### Example Usage:

```go
package main

import (
	"fmt"
	"github.com/gin-gonic/gin"
	"github.com/gagliardetto/gzip"
)

func main() {
	router := gin.Default()
	router.Use(gzip.Gzip(gzip.BestSpeed))
	router.GET("/bench", func(cc *gin.Context) {
			cc.IndentedJSON(200, gin.H{
			  "abcdefghijklmnopqrstuvwxyz0":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz1":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz2":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz3":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz4":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz5":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz6":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz7":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz8":  12345678910111213141516171819202122232425262728293031323334353637383940,
			  "abcdefghijklmnopqrstuvwxyz9":  12345678910111213141516171819202122232425262728293031323334353637383940,
			})
	})

	router.Run(":8080")
}
```

