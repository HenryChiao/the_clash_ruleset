# The Clash Ruleset

<div align="center">

![GitHub last commit](https://img.shields.io/github/last-commit/HenryChiao/the_clash_ruleset)
![GitHub stars](https://img.shields.io/github/stars/HenryChiao/the_clash_ruleset)
![GitHub forks](https://img.shields.io/github/forks/HenryChiao/the_clash_ruleset)
![License](https://img.shields.io/github/license/HenryChiao/the_clash_ruleset)

**Curated Mihomo/Clash Ruleset Collection**

High-quality routing rules personally collected and maintained

English | [简体中文](./README.md)

</div>

---

## 📋 Introduction

A comprehensive collection of Mihomo/Clash Meta routing rules, organized by region and purpose for flexible modular deployment.

### Key Features

- ✅ **Modular Design** - Categorized by region and use case for flexible configuration
- ✅ **Regular Updates** - Periodic verification and updates for rule validity
- ✅ **Battle-Tested** - All rules verified through real-world testing
- ✅ **Ready to Use** - Compatible with multiple proxy tools

---

## 📦 Rule Categories

### 📍 Location-Based Rules

**Directory**: [`The_Location_rule-set/`](./The_Location_rule-set/)

Includes the following rule types:
- 📱 **Wi-Fi Calling** - 15 countries/regions, 40+ carriers
- 🏦 **Banking Services** - Major banks in Hong Kong & USA
- 🍎 **Apple Services** - Location detection, etc.

For detailed rule list and usage guide, please refer to: [The_Location_rule-set/README.md](./The_Location_rule-set/README.md)

---

## 🚀 Quick Start

### Mihomo / Clash Meta Configuration

```yaml
rule-providers:
  # Example: US Wi-Fi Calling
  wificalling-us:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/wificalling-us.list"
    path: ./ruleset/wificalling-us.yaml
    interval: 86400

proxy-groups:
  - name: "🇺🇸 US"
    type: select
    # Your proxy nodes

rules:
  - RULE-SET,wificalling-us,🇺🇸 US
```

### CDN Acceleration (Recommended for China)

```yaml
url: "https://cdn.jsdelivr.net/gh/HenryChiao/the_clash_ruleset@main/The_Location_rule-set/wificalling-us.list"
```

**More configuration examples and detailed instructions**: [The_Location_rule-set/README.md](./The_Location_rule-set/README.md)

---

## 💡 Important Notes

### ⚠️ Wi-Fi Calling Configuration

**Wi-Fi Calling should use corresponding country nodes, NOT direct connection**

```yaml
# ✅ Correct
- RULE-SET,wificalling-us,🇺🇸 US Node

# ❌ Wrong
- RULE-SET,wificalling-us,DIRECT
```

For detailed explanation and configuration guide, please check the README in the folder.

---

## 📊 Coverage

| Type | Coverage |
|------|----------|
| Wi-Fi Calling | 15 countries/regions, 40+ carriers |
| Banking Services | Hong Kong & USA, 31 institutions |
| Total Rules | 200+ |

---

## 🔗 Links

- 📖 [Detailed Documentation](./The_Location_rule-set/README.md)
- 🐛 [Issue Tracker](https://github.com/HenryChiao/the_clash_ruleset/issues)
- 💬 [Discussions](https://github.com/HenryChiao/the_clash_ruleset/discussions)

---

## 🤝 Contributing

Issues and Pull Requests are welcome!

To add new rules, please provide:
- Detailed technical information (domains, IP ranges, MCC/MNC, etc.)
- Testing verification results

---

## 📝 Changelog

### 2026-01-07
- ✅ Project initialization
- ✅ Added location-based rulesets (Wi-Fi Calling + Banking)

---

## 📄 License

This project is licensed under the [MIT License](./LICENSE)

---

## ⚠️ Disclaimer

- This ruleset is for educational and research purposes only
- Please test before use
- Users assume all risks
- Comply with local laws and regulations

---

<div align="center">

**If this project helps you, please give it a ⭐ Star!**

Made with ❤️ by [HenryChiao](https://github.com/HenryChiao)

</div>
