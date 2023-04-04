

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
```