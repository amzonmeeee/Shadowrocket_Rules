# Changelog

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
