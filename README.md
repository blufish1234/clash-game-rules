# Clash 遊戲規則集 🎮

一組為 Clash 及相容客戶端精心配置的規則集，專為各類遊戲與服務進行優化。

## 🛠️ 如何使用

要將這些規則應用於您的 Clash 配置，請將其新增至 `rule-providers` 部分。

### 1. 定義規則提供者 (Rule Providers)
在您的配置文件中添加以下內容：

```yaml
rule-providers:
  gryphline:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/Gryphline.yaml"
    path: ./ruleset/gryphline.yaml
    interval: 86400

  vrchat:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/VRChat.yaml"
    path: ./ruleset/vrchat.yaml
    interval: 86400
```

### 2. 應用規則
在 `rules` 部分使用這些提供者：

```yaml
rules:
  - RULE-SET,gryphline,🎮 遊戲流量
  - RULE-SET,vrchat,🌐 VRChat
  # ... 其他規則
```

## 📦 已提供的規則

| 圖標 | 名稱 | 描述 | 規則集類型 |
| :---: | :--- | :--- | :--- |
| <img src="icons/gryphline.png" width="32"> | **Gryphline** | 適用於 Gryphline 服務及遊戲（例如：明日方舟：終末地）。 | `classical` |
| <img src="icons/vrchat.png" width="32"> | **VRChat** | 為 VRChat 實例、資源載入優化的路由規則。 | `classical` |

## 📦 sing-box 規則集

本專案也提供 sing-box 格式的規則集，存放在 `sing-box/` 目錄中。

### 如何使用

在 sing-box 配置中添加遠端規則集：

```json
{
  "route": {
    "rule_set": [
      {
        "type": "remote",
        "tag": "gryphline",
        "format": "source",
        "url": "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/sing-box/Gryphline.json"
      },
      {
        "type": "remote",
        "tag": "vrchat",
        "format": "source",
        "url": "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/sing-box/VRChat.json"
      }
    ],
    "rules": [
      {
        "rule_set": "gryphline",
        "outbound": "遊戲流量"
      },
      {
        "rule_set": "vrchat",
        "outbound": "VRChat"
      }
    ]
  }
}
```

> **注意：** sing-box 的 Headless Rule 不支援 `IP-ASN`，因此 VRChat 規則集中的 `IP-ASN,199524`（G-Core Labs）已轉換為對應的 IP-CIDR 前綴。

## 🎨 資源資訊
每個服務的圖標都存放在 `icons/` 目錄中。您可以在 Clash 面板（如 Yacd 或 Clash Verge）中通過指向該圖標的 URL 來使用它們。

## 🤝 貢獻
如果您想添加更多遊戲規則或改進現有規則，歡迎提交 Issue 或 Pull Request。
