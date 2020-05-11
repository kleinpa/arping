[![pkg.go.dev](https://godoc.org/github.com/j-keck/arping?status.svg)](https://pkg.go.dev/github.com/j-keck/arping)

# Arping

Arping is a native go library for sending and receiving ARP datagrams on Linux and BSD systems.

It can be used to resolve MAC addresses and broadcast gratuitous ARPs.

## Usage

```shell
go get github.com/j-keck/arping
```

```go
import (
	"log"
	"net"

	"github.com/j-keck/arping"
)

func main() {
	dstIP := net.ParseIP("192.168.1.1")
	if hwAddr, duration, err := arping.Ping(dstIP); err != nil {
		log.Fatal(err)
	} else {
		log.Printf("%s (%s) %d usec\n", dstIP, hwAddr, duration/1000)
	}
}
```

The library requires raw socket access. It must run as root, or with appropriate capabilities under linux:
```shell
sudo setcap cap_net_raw+ep <BIN>
```

## Binary

A binary is provided in `cmd/arping` that broadcasts an ARP request for the provided address and display information about the response.
