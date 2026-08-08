# HK_Rules

給香港網絡環境的自用 Shadowrocket 分流配置。

這個 repository 只維護一個配置檔：`HK_Rules.conf`。它只把在香港沒有官方支援的 OpenAI / ChatGPT / Sora 與 Anthropic / Claude 服務交給 `PROXY`，其他流量一律 `DIRECT`。

## 直接使用

1. 在 Shadowrocket 中加入你的節點或訂閱。
2. 匯入 [`HK_Rules.conf`](HK_Rules.conf)。
3. 如果你的代理策略名稱不是 `PROXY`，把配置內的 `PROXY` 改成實際策略名稱。
4. 先測試 ChatGPT 與 Claude，再按需要調整節點出口。

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

- OpenAI、ChatGPT、Sora、OpenAI 靜態資源與使用者內容域名
- Anthropic、Claude、Claude 使用者內容域名

這是以域名為基礎的分流，不能保證涵蓋第三方整合服務或硬編碼 IP。服務的香港支援地區、域名和連線方式可能改變，請自行驗證。

## 設計原則

- 只保留一個自用配置，不提供節點、訂閱、帳號或憑證。
- 不依賴第三方遠端規則集，避免上游規則變動造成意外代理。
- OpenAI 與 Claude 的服務可用地區請以其官方文件為準：[ChatGPT 支援地區](https://help.openai.com/en/articles/7947663-chatgpt-supported-countries)、[Claude 可用地區](https://support.claude.com/en/articles/8461763-where-can-i-access-claude)。

請自行確認節點來源、當地法律及各服務的使用條款。

## License

本 repository 採用 [MIT License](LICENSE)。
