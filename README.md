# clash-game-rules

A collection of rule sets for [Mihomo](https://github.com/MetaCubeX/mihomo) (formerly Clash Meta) and compatible clients (e.g. Clash Verge Rev), tailored for games and specific services. sing-box equivalents are also provided.

---

## 📋 Rule Sets

| Icon | Name | File | Description |
| :---: | :--- | :--- | :--- |
| <img src="icons/gryphline.png" width="28"> | **Gryphline** | [`Gryphline.yaml`](Gryphline.yaml) | Covers Gryphline services and games (e.g. Arknights: Endfield). |
| <img src="icons/vrchat.png" width="28"> | **VRChat** | [`VRChat.yaml`](VRChat.yaml) | Domains, CDN IPs, and ASN for VRChat and its dependencies (Photon, G-Core Labs). |
| — | **Discord** | [`discord.yaml`](discord.yaml) | Discord domains and precise voice server IP ranges (Cloudflare + i3D.net). |
| — | **Claude** | [`claude.yaml`](claude.yaml) | Anthropic/Claude domains, CDN, auth, telemetry, and ASN/IP ranges. |

---

## 🚀 Usage

### Clash / Clash Meta

Add entries to `rule-providers` in your config, then reference them in `rules`.

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

  discord:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/discord.yaml"
    path: ./ruleset/discord.yaml
    interval: 86400

  claude:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/claude.yaml"
    path: ./ruleset/claude.yaml
    interval: 86400

rules:
  - RULE-SET,gryphline,<proxy-group>
  - RULE-SET,vrchat,<proxy-group>
  - RULE-SET,discord,<proxy-group>
  - RULE-SET,claude,<proxy-group>
```

### sing-box

Rule sets in sing-box source format are available in the [`sing-box/`](sing-box/) directory.

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
      },
      {
        "type": "remote",
        "tag": "discord",
        "format": "source",
        "url": "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/sing-box/discord.json"
      },
      {
        "type": "remote",
        "tag": "claude",
        "format": "source",
        "url": "https://raw.githubusercontent.com/blufish1234/clash-game-rules/main/sing-box/claude.json"
      }
    ],
    "rules": [
      { "rule_set": "gryphline", "outbound": "<outbound>" },
      { "rule_set": "vrchat",    "outbound": "<outbound>" },
      { "rule_set": "discord",   "outbound": "<outbound>" },
      { "rule_set": "claude",    "outbound": "<outbound>" }
    ]
  }
}
```

> **Note:** sing-box Headless Rules do not support `IP-ASN`. The `IP-ASN` entries in VRChat (`199524`) and Claude (`399358`) have been expanded to their corresponding IP-CIDR prefixes in the sing-box versions.

---

## 📁 Repository Structure

```
clash-game-rules/
├── Gryphline.yaml        # Clash rule set — Gryphline
├── VRChat.yaml           # Clash rule set — VRChat
├── discord.yaml          # Clash rule set — Discord (domains + voice IPs)
├── claude.yaml           # Clash rule set — Claude / Anthropic
├── icons/
│   ├── gryphline.png
│   └── vrchat.png
└── sing-box/
    ├── Gryphline.json    # sing-box rule set — Gryphline
    ├── VRChat.json       # sing-box rule set — VRChat
    ├── discord.json      # sing-box rule set — Discord
    └── claude.json       # sing-box rule set — Claude / Anthropic
```

---

## 🤝 Contributing

Pull requests are welcome. If you'd like to add rules for a new service or fix existing entries, please open an issue or PR.
