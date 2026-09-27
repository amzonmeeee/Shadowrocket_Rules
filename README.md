# HK_Rules

給香港網絡環境的自用 Shadowrocket 分流配置。

[![Validate configuration](https://github.com/amzonmeeee/Shadowrocket_Rules/actions/workflows/validate.yml/badge.svg)](https://github.com/amzonmeeee/Shadowrocket_Rules/actions/workflows/validate.yml)

這個 repository 只維護一個配置檔：`HK_Rules.conf`。它只把在香港沒有官方支援的 OpenAI / ChatGPT / Sora 與 Anthropic / Claude 服務交給 `PROXY`，其他流量一律 `DIRECT`。

## 直接使用

1. 在 Shadowrocket 中加入你的節點或訂閱。
2. 匯入 [`HK_Rules.conf`](HK_Rules.conf)。
3. 如果你的代理策略名稱不是 `PROXY`，把配置內的 `PROXY` 改成實際策略名稱。
4. 先測試 ChatGPT 與 Claude，再按需要調整節點出口。

GitHub Raw 檔案地址：

```text
https://raw.githubusercontent.com/amzonmeeee/Shadowrocket_Rules/main/HK_Rules.conf
```

也可以直接掃描 [`assets/qr/HK_Rules.png`](assets/qr/HK_Rules.png) 匯入。

![HK_Rules import QR Code](assets/qr/HK_Rules.png)

## 分流邏輯

| 流量 | 策略 |
| --- | --- |
| 本機、私有網絡與 `.local` | `DIRECT` |
| OpenAI / ChatGPT / Sora | `PROXY` |
| Anthropic / Claude | `PROXY` |
| 其他所有流量 | `DIRECT` |

Shadowrocket 會按 `[Rule]` 由上至下匹配，命中第一條後停止；配置最後的 `FINAL,DIRECT` 是全域直連兜底。

## 規則範圍

目前代理的域名包括：

- OpenAI、ChatGPT、Sora、ChatGPT Sites、語音服務、專用驗證與內容主機
- Anthropic、Claude、Claude Desktop 預覽、MCP、專用登入與內容主機
- Anthropic 官方公布的接入 IPv4／IPv6，供直接以 IP 連線時匹配

### 規則來源與取捨（2026-09-28）

| 對照來源 | 本配置採納的範圍 |
| --- | --- |
| [Anthropic Desktop 網絡要求](https://code.claude.com/docs/en/desktop#network-access-requirements)、[Claude Code 網絡要求](https://code.claude.com/docs/en/network-config#network-access-requirements) | 官方列出的 Anthropic／Claude 專屬域名及子域名；主要登入、API、下載、連接器、預覽主機均由後綴規則涵蓋。 |
| [Anthropic 接入 IP 文件](https://platform.claude.com/docs/en/api/ip-addresses) | 加入接收入站連線的 `160.79.104.0/23` 與 `2607:6bc0::/48`，均使用 `no-resolve`；用於 Anthropic 對外呼叫的出站 `/21` 不屬於用戶端目標地址。 |
| [v2fly Anthropic](https://github.com/v2fly/domain-list-community/blob/master/data/anthropic)、[MetaCubeX Anthropic](https://github.com/MetaCubeX/meta-rules-dat/blob/meta/geo/geosite/anthropic.list)、[Claude Core](https://github.com/erwanjun/surge-claude-rules/blob/main/Surge/Claude-Core.list) | 補上 `clau.de`、`claudemcpclient.com` 及精確的 Anthropic 驗證／CDN 主機。 |
| [v2fly OpenAI](https://github.com/v2fly/domain-list-community/blob/master/data/openai)、[blackmatrix7 OpenAI](https://github.com/blackmatrix7/ios_rule_script/blob/master/rule/Shadowrocket/OpenAI/OpenAI.list) | 補上 `chat.com`、`chatgpt.site`、`oaistatsig.com`、專用語音、驗證、CDN 及動態 WebSocket 主機。 |
| [ACL4SSR Claude](https://github.com/ACL4SSR/ACL4SSR/blob/master/Clash/Ruleset/Claude.list)、[blackmatrix7 Claude](https://github.com/blackmatrix7/ios_rule_script/blob/master/rule/Shadowrocket/Claude/Claude.list)、[Sukka AI](https://ruleset.skk.moe/List/non_ip/ai.conf) | 核對常見基礎域名；Sukka 是多個 AI 服務的混合清單，不整份匯入。 |

Google Storage、npm、GitHub Raw、Cloudflare 驗證、Auth0、Stripe、Sentry、Datadog、通用 LiveKit 主機等會由其他服務共用；這份按目的地分流的配置不會代理整個供應商網域。Claude Code 的安裝、第三方連接器或某些網頁功能因此仍可能產生直連請求。

這份配置以域名規則為主，另加 Anthropic 官方接入 IP。它不能保證涵蓋第三方整合服務、其他硬編碼 IP，或沒有經過 Shadowrocket 的應用程式及系統連線。匯入後可在 Shadowrocket 的連線記錄核對 Claude 網頁、桌面版、Claude Code 及 ChatGPT 的實際命中策略和出口；若 `PROXY` 會自動切換節點，也要核對實際出口。掃描二維碼或使用 Raw 連結的配置亦須重新更新。

## 設計原則

- 只保留一個自用配置，不提供節點、訂閱、帳號或憑證。
- 不依賴第三方遠端規則集，避免上游規則變動造成意外代理。
- OpenAI 與 Claude 的服務可用地區請以其官方文件為準：[ChatGPT 支援地區](https://help.openai.com/en/articles/7947663-chatgpt-supported-countries)、[Claude 可用地區](https://support.claude.com/en/articles/8461763-where-can-i-access-claude)。
- 分流規則只控制網絡路徑，不能保證帳號安全或符合服務條款。Anthropic 會用 IP 及其他訊號判斷地區，並把在不支援地區建立帳號列為可能停權原因；請參閱[地區判斷說明](https://privacy.claude.com/en/articles/11186740-does-claude-use-my-location)及[停權與申訴說明](https://support.claude.com/en/articles/8241253-safeguards-warnings-and-appeals)。

請自行確認節點來源、當地法律及各服務的使用條款。

## License

本 repository 採用 [MIT License](LICENSE)。
