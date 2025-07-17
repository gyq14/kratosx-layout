# kratos-layout 使用说明（基于 kratosx 模板）

## 1. 项目简介

本项目为基于 [kratosx](https://github.com/gyq14/kratosx) 的微服务项目模板，适用于通过 kratosx CLI 快速初始化、开发和管理 Go 微服务。kratosx 提供一站式的项目脚手架、代码生成、服务治理、配置管理、中间件、常用库等能力。

---

## 2. 目录结构说明

- `api/`         —— proto 文件目录，定义服务 API、消息、错误码等
- `cmd/`         —— 各服务入口（main.go）
- `internal/`    —— 业务实现（service、biz、data、conf等）
- `third_party/` —— 三方 proto 依赖
- `static/`      —— 静态资源（如有）
- `go.mod`       —— Go 依赖管理
- `README.md`    —— 项目说明

> 具体结构可根据 kratosx new 生成的模板自动调整。

---

## 3. 环境准备

- Go 1.18 及以上
- protoc 及相关插件（见下方安装指令）

### 3.1 安装 kratosx 及插件

```bash
go install github.com/gyq14/kratosx/cmd/kratosx@latest
# 常用代码生成插件
go install github.com/gyq14/kratosx/cmd/protoc-gen-go-httpx@latest
go install github.com/gyq14/kratosx/cmd/protoc-gen-go-errorsx@latest
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
go install github.com/google/gnostic/cmd/protoc-gen-openapi@latest
go install github.com/envoyproxy/protoc-gen-validate@latest
```
> 安装后请确保 `$GOPATH/bin` 已加入环境变量 `PATH`。

---

## 4. 常用 kratosx 指令

### 4.1 创建新项目

```bash
kratosx new myservice
```
- 支持参数：`--repo-url`（模板仓库）、`--branch`（分支）、`--timeout`、`--nomod` 等

### 4.2 proto 相关代码生成

- **添加 proto API 模板**
  ```bash
  kratosx proto add helloworld/v1/hello.proto
  ```
- **生成 proto 客户端代码**
  ```bash
  kratosx proto client api/helloworld.proto
  ```
- **生成 proto 服务端实现**
  ```bash
  kratosx proto server api/helloworld.proto --target-dir=internal/service
  ```
- **生成 openapi 文档**
  ```bash
  protoc --openapi_out=. api/helloworld.proto
  ```

### 4.3 项目运行与管理

- **运行服务**
  ```bash
  kratosx run
  ```
- **升级工具链**
  ```bash
  kratosx upgrade
  ```
- **查看变更日志**
  ```bash
  kratosx changelog
  ```
- **启动 Web 工具服务**
  ```bash
  kratosx webutil 8080
  ```

---

## 5. 典型开发流程

1. 创建新项目
   ```bash
   kratosx new myservice
   cd myservice
   ```
2. 添加 proto API
   ```bash
   kratosx proto add helloworld/v1/hello.proto
   ```
3. 生成 proto 客户端/服务端代码
   ```bash
   kratosx proto client api/helloworld.proto
   kratosx proto server api/helloworld.proto --target-dir=internal/service
   ```
4. 运行服务
   ```bash
   kratosx run
   ```
5. 升级工具链
   ```bash
   kratosx upgrade
   ```

---

## 6. 中间件与服务治理

kratosx 内置丰富的中间件和服务治理能力，支持认证、JWT、限流、链路追踪、日志、注册发现、健康检查、Prometheus 监控、pprof 性能分析等。

- **中间件接入**：在 internal/service 或 main.go 中引入所需中间件，参考 kratosx 文档。
- **服务治理**：支持 Consul、Nacos、Apollo 等注册发现与配置中心，支持 Prometheus 监控。

---

## 7. 配置管理

- 支持本地文件、环境变量、远程配置中心（Nacos、Apollo、Consul等）
- 支持配置热加载与动态变更
- 配置文件一般位于 `internal/conf/` 目录

---

## 8. 代码生成插件说明

- **protoc-gen-go-httpx**：生成 http 端代码
- **protoc-gen-go-errorsx**：生成全局 error 代码
- **protoc-gen-go**：生成 pb 代码
- **protoc-gen-go-grpc**：生成 grpc 代码
- **protoc-gen-openapi**：生成 openapi.yaml
- **protoc-gen-validate**：生成参数校验代码

---

## 9. 常见问题

- 依赖安装失败：请检查 Go 版本和 GOPROXY 设置
- proto 编译报错：确认 protoc 及插件已正确安装，路径无误
- 端口冲突：修改 conf.yaml 或启动参数
- 配置文件未加载：确保挂载路径正确，文件格式无误

---

## 10. 参考文档

- [kratosx README](https://github.com/gyq14/kratosx/blob/main/README.md)
- [Protocol Buffers 官方文档](https://developers.google.com/protocol-buffers)

如需进一步细化某一部分（如 CI/CD、灰度发布、日志采集等），请补充说明你的需求！
