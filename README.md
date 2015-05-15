## DUPLICATE


```bash
mkdir -p projB/src/projB
> projB/src/projB/foo.go <<EOF
package projB
const (
  PROJB = true
  )
EOF

mkdir -p projA/src/projA
> projA/src/projA/main.go <<EOF
package main

import (
  "fmt"
  "projB"
)

func main() {
  fmt.Println(projB.PROJB)
}
EOF

cd projB
git init .
git add -A .
git commit -am "INIT B"

git subtree split --prefix=src/projB --branch=export

cd ../projA
git init .
git add -A .
git commit -am "INIT A"

git remote add projb -f ../projB
git subtree add --prefix=vendor/src/projB projB/export --message="import projB"
```
