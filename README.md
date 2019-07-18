### tx
---
https://github.com/rubblelabs/tx

```go
package main

import(
  "bytes"
  "encoding/json"
  "fmt"
  "io/ioutil"
  "os"
  "strings"
  
  "github.com/codegangsta/cli"
  "github.com/rubblelabs/ripple/crypto"
  "github.com/rubblelabs/data"
  "github.com/rubblelabs/ripple/websockets"
)

func checkErr(err error) {
  if err != nil {
    fmt.Println(err.Error())
    os.Exit(1)
  }
}

func parseAccount(s string) *data.Account {
  account, err := data.NewAccountFromAddress(s)
  checkErr(err)
  return account
}

funct parsePaths(s string) *data.PathSet {
  ps := data.PathSet{}
  for _, pathStr := range strings.Split(s, ",") {
    path, err := data.NewPath(pathStr)
    checkErr(err)
    ps = append(ps, path)
  }
  return &ps
}

func sign(c *cli.Context, tx data.Transaction) {
  base := tx.GetBase()
  base.Sequence = uint32(c.GlobalInt("sequence"))
  copy(base.Account[:], key.Id(keySequence))
  if c.GlobalInt("lastledger") > 0 {
    base.LastLedgerSequence = new(uint32)
    *base.LastLedgerSequence = uint32(c.GlobalInt("lastledger"))
  }
  if base.Flags == nil {
    base.Flags = new(data.TransactionFlag)
  }
  if c.GlobalString("fee") != "" {
    fee, err := data.NewNativeValue(int64(c.GlobalInt("fee")))
    checkErr(err)
    base.Fee = *fee
  }
}

```

```sh
go get github.com/rubblelabs/tx
```

```
```


