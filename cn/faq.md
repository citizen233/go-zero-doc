# 常见问题集合

1. goctl安装了执行命令却提示 `command not found: goctl` 字样。
   > 如果你通过 `go get` 方式安装，那么 `goctl` 应该位于 `$GOPATH` 中，
   > 你可以通过 `go env GOPATH` 查看完整路径，不管你的 `goctl` 是在 `$GOPATH`中，
   > 还是在其他目录，出现上述问题的原因就是 `goctl` 所在目录不在 `PATH` (环境变量)中所致。

1. rpc怎么调用
   > 该问题可以参考快速开始中的[rpc编写与调用](rpc-call.md)介绍，其中有rpc调用的使用逻辑。

1. proto使用了import，goctl命令需要怎么写。
   > `goctl` 对于import的proto指定 `BasePath` 提供了 `protoc` 的flag映射，即 `--proto_path, -I`，
   > `goctl` 会将此flag值传递给 `protoc`.

1. 假设 `base.proto` 的被main proto 引入了，为什么不生能生成`base.pb.go`。
   > 对于 `base.proto` 这种类型的文件，一般都是开发者有message复用的需求，他的来源不止有开发者自己编写的`proto`文件，
   > 还有可能来源于 `google.golang.org/grpc` 中提供的一些基本的proto,比如 `google/protobuf/any.proto`, 如果由 `goctl`
   > 来生成，那么就失去了集中管理这些proto的意义。

1. model怎么控制缓存时间
   > 在 `sqlc.NewNodeConn` 的时候可以通过可选参数 `cache.WithExpiry` 传递，如缓存时间控制为1天，代码如下:
   > ```go
   > sqlc.NewNodeConn(conn,redis,cache.WithExpiry(24*time.Hour))  
   > ```
   
1. jwt鉴权怎么实现
   > 请参考[jwt鉴权](jwt.md)

1. api中间件怎么使用
   > 请参考[中间件](middleware.md)

faq会不定期更新大家遇到的问题，也欢迎大家把常见问题通过pr写在这里。