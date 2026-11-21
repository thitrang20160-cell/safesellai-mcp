# SafeSellAI MCP

**上架前先查一遍：给 AI Agent 用的跨境电商侵权排查引擎。**
Pre-listing IP risk checks for AI agents — trademark terms, TRO litigation, image similarity, listing scoring and store audits, before a product goes live on Walmart / Amazon.

SafeSellAI 把侵权排查能力开放为 [Model Context Protocol](https://modelcontextprotocol.io) 工具：你的 Agent 在上架、选品、改 listing 之前先调一遍，拿到「能卖 / 要改 / 不能卖」的判定和理由，再继续干活。

> 本仓库是该 MCP 服务的**公开说明与接入仓库**：服务端为托管服务，源码不开源。

- **远程端点**：`https://safesellai.com/mcp`（Streamable HTTP，零安装）
- **接入文档**：https://safesellai.com/mcp-guide （公开，无需登录，含各客户端配置片段）
- **免注册试用**：不带 Key 即可用文字排查（见下方免费层）；带 API Key 解锁全部工具与更高额度，Key 在 https://safesellai.com 账号设置中创建

## 能做什么

- **商标词排查**：标题 / 五点 / 描述粘贴即查，自动匹配侵权词并给出判定与可解释原因（中英双语、美欧商标）
- **TRO 案件查询**：查某个词 / 品牌是否正卷入美国 TRO 诉讼、案件是否在诉
- **图片检查**：单图查外观专利与图库相似风险
- **Listing 多维评分**：一个 listing 的文字 + 图片综合风险分
- **店铺体检**：自带商品清单批量排查（items 模式），输出风险汇总

代表性工具：`check_brand`（查品牌词）、`check_batch`（批量排查）、`check_tro`（查 TRO）、`check_image`（查图）、`store_audit`（店铺体检）。完整工具清单与参数见接入文档，或连上端点后调用 `tools/list` 查看（免 Key 可浏览）。

## 免费层

| 方式 | 可用范围 |
| --- | --- |
| 免注册（无 Key） | `check_brand` / `check_batch` / `check_tro` 文字排查，100 词/天/IP；`tools/list` 浏览全部工具 |
| 注册拿 Key | 全部工具（含查图、店铺体检）+ 更高额度；完成首次排查任务可解锁额外免费体检次数 |

## 快速接入

```json
{
  "mcpServers": {
    "safesellai": {
      "url": "https://safesellai.com/mcp",
      "headers": { "Authorization": "Bearer <YOUR_SAFESELLAI_API_KEY>" }
    }
  }
}
```

免注册试用时把 `headers` 整段删掉即可。Claude Code：

```bash
claude mcp add --transport http safesellai https://safesellai.com/mcp
```

接入后先调用 `start_here`，它会介绍能力地图并引导完成第一次排查。

## 相关

- 塞星铺货执行 MCP（调用本引擎完成采集 → 排查 → 上架全流程）：https://github.com/thitrang20160-cell/saixing-listing-mcp
- 跨境电商 MCP 导航「MCP 码头」：https://safesellai.com/mcp-nav/

## License

MIT — see [LICENSE](LICENSE). 托管服务由 SafeSellAI（中山心一出海科技有限公司）运营；商标与品牌归其所有。
