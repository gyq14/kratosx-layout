## 典型使用流程

1. **创建新项目**
   ```bash
   kratosx new myservice
   cd myservice
   go generate ./...
   go build -o ./bin/ ./...
   ./bin/myservice -conf ./configs
   ```
2. **安装远程模块**
   ```bash
    go install github.com/gyq14/kratosx/cmd/kratosx@latest
    go install github.com/gyq14/kratosx/cmd/protoc-gen-go-httpx@latest
    go install github.com/gyq14/kratosx/cmd/protoc-gen-go-errorsx@latest
   ```

3. **添加 proto API**
   ```bash
   kratosx proto add helloworld/v1/hello.proto
   ```
4. **生成 proto 客户端/服务端代码**
   ```bash
   kratosx proto client api/helloworld.proto
   kratosx proto server api/helloworld.proto --target-dir=internal/service
   ```
5. **运行服务**
   ```bash
   kratosx run
   ```
6. **升级工具链**
   ```bash
   kratosx upgrade
   ```
