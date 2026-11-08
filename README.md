# opencode-axonhub-tracing

OpenCode 插件：为每次 LLM 请求注入 trace headers。

默认 header key 对齐 AxonHub：

- `AH-Thread-Id` ← OpenCode `sessionID`
- `AH-Trace-Id` ← OpenCode `message.id`

同时保持通用能力：header key 可通过环境变量覆盖。

## 项目来源与维护

本项目 fork 自 [looplj/opencode-axonhub-tracing](https://github.com/looplj/opencode-axonhub-tracing)。我们向原上游提交的 PR 已数月未获回应。为持续推进开发与修复，本 fork 后续由 infituit 相关成员独立维护并发布，不以上游合并 PR 为前提。

当前维护仓库为 [infituit/opencode-axonhub-tracing](https://github.com/infituit/opencode-axonhub-tracing)。问题反馈与贡献请提交至该仓库的 [Issues](https://github.com/infituit/opencode-axonhub-tracing/issues) 和 Pull Requests。

**维护原则：不继承历史债务。** 不会为了维持历史兼容性而保留已知问题或延续不合理设计；必要时接受不兼容变更。

历史作者和贡献者的归属信息予以保留，见 [NOTICE](./NOTICE)。本声明说明后续维护责任，不代表原作者版权的转让。

## 安装

```bash
npm install -g opencode-axonhub-tracing
# 或
bun add -g opencode-axonhub-tracing
```

## 启用插件

在 `opencode.json` 中添加：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-axonhub-tracing"]
}
```

## 配置（可选）

默认 key：

- `AH-Thread-Id`
- `AH-Trace-Id`

可用环境变量覆盖：

- `OPENCODE_AXONHUB_TRACING_THREAD_HEADER`
- `OPENCODE_AXONHUB_TRACING_TRACE_HEADER`

示例：

```bash
export OPENCODE_AXONHUB_TRACING_THREAD_HEADER="X-Thread-Id"
export OPENCODE_AXONHUB_TRACING_TRACE_HEADER="X-Trace-Id"
```

说明：空字符串会自动回退到默认 key。

## 行为说明

- Thread ID：使用 OpenCode 的 `sessionID`
- Trace ID：使用 OpenCode 当前用户消息 `message.id`
- 若当前消息没有 `id`，仅注入 thread header

## 开发

```bash
bun install
bun test
bun run build
```
