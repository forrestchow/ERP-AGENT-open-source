# 会话同步

本目录保存 **Claude Code 可恢复会话**（`claude --resume` / `claude --resume <session-id>`）所需的 JSONL 快照。

- 来源目录：`C:\Users\Administrator\.claude\projects\E--erp-agent--\`
- 项目工作目录：`E:\erp-agent测试`
- 快照时间：2026-11-20 17:39（本地，UTC+8），即 `2026-11-20T09:39:07Z`
- 文件完整性：`manifest.json` 记录每个文件的字节数、行数、时间范围和 SHA-256

## 文件清单

| 文件 | 会话 ID | 时间范围（UTC） | 大小 | 内容概要 |
|---|---|---|---:|---|
| `0c038b7b-d120-4f25-a91b-a547ea1e9ac7.jsonl` | `0c038b7b-d120-4f25-a91b-a547ea1e9ac7` | 2026-11-20 07:23 – 09:39 | 1.52 MB | 当前会话：项目理解、harness 路由/评审分析、会话同步 |
| `1a5c9753-32c4-4c10-92eb-3376dc837ef1.jsonl` | `1a5c9753-32c4-4c10-92eb-3376dc837ef1` | 2026-11-20 07:16 – 07:21 | 1.87 MB | “分析当前项目” |
| `7700cfdc-5424-446c-822e-ca683f6bf645.jsonl` | `7700cfdc-5424-446c-822e-ca683f6bf645` | 2026-11-16 02:25 – 2026-11-20 08:39 | 5.52 MB | 项目分析、主/子 Agent 循环、历史开发会话 |

## 恢复方法

### Windows（原路径）

1. 确保项目仍在 `E:\erp-agent测试`。
2. 把本目录下的三个 `.jsonl` 复制到：
   `C:\Users\<用户名>\.claude\projects\E--erp-agent--\`
3. 在 `E:\erp-agent测试` 目录运行：

   ```bash
   claude --resume
   ```

   在列表中选择会话；或直接指定会话 ID：

   ```bash
   claude --resume 0c038b7b-d120-4f25-a91b-a547ea1e9ac7
   ```

### 其他机器或项目路径

Claude Code 的会话目录名由启动时的工作目录编码而来，例如：

```text
E:\erp-agent测试  →  E--erp-agent--
```

编码规则通常是把非字母数字字符替换为 `-`。如果项目路径不同，请把 JSONL 放到该路径对应的会话目录下；否则 `--resume` 列表不会显示这些会话。以 Claude Code 实际生成的目录名为准。

## 注意事项

- **这是快照，不是实时同步。** 复制时 `0c038b7b` 会话仍在写入，快照之后的新消息（包括本次提交/推送过程）不会出现在文件中。后续可重新执行同步。
- **内容范围。** JSONL 包含完整对话、工具调用及其输出，以及 `api-request-blob` 等会话元数据，这是 Claude Code 恢复会话的正常组成部分。
- **未包含的内容。** 不包含 `.claude/projects/E--erp-agent--/memory/`、全局配置、API Key 或登录态。
- **公开仓库提醒。** 当前仓库是 public。同步前已扫描常见凭据格式（`sk-*`、GitHub token、Mongo URI、私钥、JWT、密码赋值等），未发现真实凭据；但会话记录仍可能包含业务数据、内部路径和代码片段，公开前请自行复核，并避免在会话中粘贴密钥。
- `manifest.json` 中的 SHA-256 对应本次快照；源文件在快照后继续增长属于正常现象。
