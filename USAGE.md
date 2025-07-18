## 典型使用流程

1. **创建新项目**
   ```bash
   kratosx new myservice
   go mod tidy
   ```
2. **升级工具链**
   ```bash
   kratosx upgrade
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

