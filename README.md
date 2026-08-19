# The Clash Ruleset

<div align="center">

![GitHub last commit](https://img.shields.io/github/last-commit/CherryMian/the_clash_ruleset)
![GitHub stars](https://img.shields.io/github/stars/CherryMian/the_clash_ruleset)
![GitHub forks](https://img.shields.io/github/forks/CherryMian/the_clash_ruleset)
![License](https://img.shields.io/github/license/CherryMian/the_clash_ruleset)

**精心维护的 Mihomo/Clash 规则集合**

个人收集整理的高质量分流规则

[English](./README_EN.md) | 简体中文

</div>

---

## 📋 项目简介

本项目维护了一套完整的 Mihomo/Clash Meta 分流规则集，按用途和地区模块化组织，支持按需加载。

### 核心特性

- ✅ **模块化设计** - 按地区和用途分类，灵活配置
- ✅ **持续更新** - 定期验证和更新规则有效性
- ✅ **实测验证** - 所有规则均经过实际测试
- ✅ **开箱即用** - 支持多种代理工具

---

## 📦 规则分类

### 📍 地区分流规则

**存放目录**: [`The_Location_rule-set/`](./The_Location_rule-set/)

包含以下类型的规则:
- 📱 **Wi-Fi Calling** - 15个国家/地区，40+运营商
- 🏦 **银行服务** - 香港、美国主要银行
- 🍎 **Apple 服务** - 地区检测等

详细规则列表和使用说明请查看: [The_Location_rule-set/README.md](./The_Location_rule-set/README.md)

---

## 🚀 快速开始

### Mihomo / Clash Meta 配置

```yaml
rule-providers:
  # 示例: 美国 Wi-Fi Calling
  wificalling-us:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/CherryMian/the_clash_ruleset/main/The_Location_rule-set/wificalling-us.list"
    path: ./ruleset/wificalling-us.yaml
    interval: 86400

proxy-groups:
  - name: "🇺🇸 美国"
    type: select
    # 你的节点配置

rules:
  - RULE-SET,wificalling-us,🇺🇸 美国
```

### CDN 加速 (国内推荐)

```yaml
url: "https://cdn.jsdelivr.net/gh/CherryMian/the_clash_ruleset@main/The_Location_rule-set/wificalling-us.list"
```

**更多配置示例和详细说明**: [The_Location_rule-set/README.md](./The_Location_rule-set/README.md)

---

## 💡 重要提示

### ⚠️ Wi-Fi Calling 配置

**Wi-Fi Calling 应使用对应国家的节点，而不是直连**

```yaml
# ✅ 正确
- RULE-SET,wificalling-us,🇺🇸 美国节点

# ❌ 错误
- RULE-SET,wificalling-us,DIRECT
```

详细原因和配置说明请查看文件夹内的 README。

---

## 📊 覆盖范围

| 类型 | 覆盖范围 |
|------|----------|
| Wi-Fi Calling | 15个国家/地区，40+运营商 |
| 银行服务 | 香港、美国，31家机构 |
| 规则总数 | 200+ |

---

## 🔗 相关链接

- 📖 [详细使用文档](./The_Location_rule-set/README.md)
- 🐛 [问题反馈](https://github.com/CherryMian/the_clash_ruleset/issues)
- 💬 [讨论交流](https://github.com/CherryMian/the_clash_ruleset/discussions)

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

如需添加新的规则，请提供:
- 详细的技术信息（域名、IP段、MCC/MNC等）
- 测试验证结果

---

## 📝 更新日志

### 2026-01-07
- ✅ 项目初始化
- ✅ 添加地区分流规则集（Wi-Fi Calling + 银行）

---

## 📄 许可证

本项目采用 [MIT License](./LICENSE)

---

## ⚠️ 免责声明

- 本规则集仅供学习交流使用
- 使用前请自行测试验证
- 使用者需自行承担使用风险
- 请遵守当地法律法规

---

<div align="center">

**如果这个项目对你有帮助，请给个 ⭐ Star！**

Made with ❤️ by [HenryChiao](https://github.com/HenryChiao)

</div>
