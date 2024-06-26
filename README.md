# Invoice Generator

A simple invoice generator created by [Quail](https://quail.ink). 

![](https://static.quail.ink/media/qz5uzv5q.webp)


## Usage

```go
package main

import (
  "os"
  "log"
  invoice "github.com/quail-ink/invoice-generator"
)

func main() {
	builder, err := invoice.NewBuilder(Config{},"./sample-params-1.yaml")
	if err != nil {
		log.Panic("failed to create builder")
	}

	buf, err := builder.GenerateInvoice()
	if buf == nil || err != nil {
		log.Panic("failed to generate invoice")
	}

	filename := "sample-invoice.pdf"
	if err := os.WriteFile(filename, buf, 0666); err != nil {
		log.Panic("failed to write to file")
	}
}
```

### Configuration

The builder can be configured with custom fonts, to display CJK characters properly. Here is an example of how to configure the builder with [NotoSansCJK-JP](https://github.com/minoryorg/Noto-Sans-CJK-JP/tree/master/fonts)

```go
builder, _ := invoice.NewBuilder(
	Config{
		FontName:       "noto-sans-cjk",
		FontNormal:     "./fonts/NotoSansCJK-JP/NotoSansCJKjp-Regular.ttf",
		FontItalic:     "./fonts/NotoSansCJK-JP/NotoSansCJKjp-Italic.ttf",
		FontBold:       "./fonts/NotoSansCJK-JP/NotoSansCJKjp-Bold.ttf",
		FontBoldItalic: "./fonts/NotoSansCJK-JP/NotoSansCJKjp-BoldItalic.ttf",
	},
	"./sample-params-2.yaml")
```
