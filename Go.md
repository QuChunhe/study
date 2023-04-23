

https://github.com/mactsouk/mastering-Go-3rd

mastering-Go-3rd


```go
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn
```

```go
go env -w GO111MODULE=off
```

```go
go build -o helloWorld hw.go

go run hw.go

go install github.com/rakyll/hey@latest

go install golang.org/x/tools/cmd/goimports@latest

goimports -l -w .

go install golang.org/x/lint/golint@latest

golint ./...

go vet ./...

golangci-lint run


go get golang.org/dl/go.1.15.6
go1.15.6 download

go1.15.6 env GOROOT

rm -rf $(go1.15.6 env GOROOT)
rm $(go env GOPATH)/bin/go1.15.6

```