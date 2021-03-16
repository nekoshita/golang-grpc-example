# golang-grpc-example

# 事前準備
- go v1.16.0
- homebrew

# インストール

```
$ brew install grpc
$ go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
$ go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
```

# GoのgRPCのコード生成に関して
https://developers.google.com/protocol-buffers/docs/reference/go-generated

helloworld/helloworld.pb.go: メッセージやシリアライズ
helloworld/helloworld_grpc.pb.go: gRPCのサーバ/クライアント

# gRPCコードを生成する
```
$ protoc --go_out=./gen --go_opt=module=github.com/nekoshita/golang-grpc-example/gen \
    --go-grpc_out=./gen --go-grpc_opt=module=github.com/nekoshita/golang-grpc-example/gen \
    protobuf/*.proto
```

# サーバー起動
```
$ go run main.go
```

# デバッグ
```
$ brew install grpcurl
$ grpcurl -proto ./protobuf/*.proto -plaintext -d '{"name": "Cat"}' localhost:50051 helloworld.Greeter/SayHello
$ grpcurl -proto ./protobuf/*.proto -plaintext localhost:50051 helloworld.Greeter/SayNothing 
```
