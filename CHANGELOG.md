# Changelog

## 0.1.5 — 2026-11-09

- 新增 Meta Muse 網站、API、Meta 登入、雲端 VM 動態子域名、共用 Facebook／CDN 及 WhatsApp 入口代理規則。
- 加入 Meta ASN `32934` 廣覆蓋兜底；一般 Facebook、WhatsApp 及同 ASN 的 Instagram 等流量亦會代理。
- 記錄官方與第三方來源、共用基礎設施的範圍，以及尚未取得實機連線記錄、第三方整合與 UDP 的驗證限制。

## 0.1.4 — 2026-10-09

- 新增 `anthropic-com.ghost.io`、`http-intake.logs.us5.datadoghq.com` 與 `browser-intake-us5-datadoghq.com` 的精確 `DOMAIN` 代理規則。
- 說明其他應用連到相同主機亦會代理；不擴大至供應商整個域名或關鍵字匹配。

## 0.1.3 — 2026-10-06

- 補上 `claude.dev`、`claude.new`、`claude.site`、`claudepages.dev`、`antspace.dev`，並加入 Anthropic ASN `399358` 兜底。
- 保留既有 `/23`、`/48`、本機／區網直連及 `FINAL,DIRECT`，共用供應商網域不作整站代理。
- 記錄 Claude 桌面／CLI 程序規則；因本機 Shadowrocket 2.2.92 未確認支援 `PROCESS-NAME`，以停用註解保留，並說明尚未實現程序全部外網流量代理。

## 0.1.2 — 2026-09-28

- 對照 Anthropic 官方文件與多套社群規則，補充 Claude 短網址、MCP、專用驗證／CDN 主機及官方接入 IPv4、IPv6。
- 補充 OpenAI／ChatGPT 專用網域、語音與內容主機，並記錄共用第三方服務的分流界限。
- 讓 CI 驗證涵蓋 `IP-CIDR6` 規則。

## 0.1.1 — 2026-09-27

- 按 Anthropic 的 Desktop 網絡要求加入 `claude.app` 和 `claudemcpcontent.com` 分流。
- 補充 Claude Code 網絡範圍、匯入後的連線驗證，以及帳號地區限制的說明。

## 0.1.0 — 2026-08-08

- 建立自用香港分流配置 `HK_Rules.conf`。
- OpenAI / ChatGPT / Sora 與 Anthropic / Claude 走 `PROXY`。
- 未命中流量一律由 `FINAL,DIRECT` 直連。
- 加入 README、MIT License 與 Git 忽略規則，方便直接發布到 GitHub。
