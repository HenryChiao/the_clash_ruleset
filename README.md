# The Clash Ruleset

个人收集和维护的 Clash 规则集合，专注于提供精确的地理位置路由规则。

## 📖 项目简介

本项目收集整理了常用的 Clash 规则集，特别是针对不同国家和地区的特定服务进行优化配置。通过使用这些规则集，您可以实现：

- 🌍 精确的地理位置路由
- 📱 特定服务的智能分流
- 🚀 优化的网络访问体验
- 🔧 灵活的规则组合

## 📁 项目结构

```
the_clash_ruleset/
├── README.md                    # 项目主文档
├── The_Location_rule-set/       # 地理位置规则集目录
│   ├── wificalling.yaml         # WiFi Calling 规则
│   ├── telegram.yaml            # Telegram 规则
│   ├── openai.yaml              # OpenAI 规则
│   └── ...                      # 其他规则文件
└── docs/
    └── USAGE.md                 # 详细使用说明
```

## 🚀 快速开始

### 1. 在 Clash 配置中添加规则集

在您的 Clash 配置文件中添加 `rule-providers` 部分：

```yaml
rule-providers:
  wificalling:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/wificalling.yaml"
    path: ./ruleset/wificalling.yaml
    interval: 86400
```

### 2. 在规则部分引用

```yaml
rules:
  - RULE-SET,wificalling,对应国家策略组
  # 其他规则...
```

## 📋 可用规则集

| 规则集名称 | 说明 | 推荐策略 |
|---------|------|---------|
| wificalling | WiFi Calling 服务 | 对应国家策略组 |
| telegram | Telegram 服务 | 代理组 |
| openai | OpenAI 服务 | 美国节点组 |

## 🔗 相关链接

- [详细使用说明](./docs/USAGE.md)
- [WiFi Calling 配置指南](./docs/USAGE.md#wifi-calling-配置)
- [问题反馈](https://github.com/HenryChiao/the_clash_ruleset/issues)

## 📝 配置示例

查看 [USAGE.md](./docs/USAGE.md) 获取完整的配置示例和详细说明。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来帮助改进这个项目！

### 贡献指南

1. Fork 本仓库
2. 创建新的分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 开启 Pull Request

## 📄 许可证

本项目采用 MIT 许可证。详见 [LICENSE](LICENSE) 文件。

## ⚠️ 免责声明

本项目仅供学习和研究使用，请勿用于非法用途。使用本项目所产生的一切后果由使用者自行承担。

## 🙏 致谢

感谢以下项目和贡献者：

- 所有为本项目做出贡献的开发者

---

**Star ⭐ 本项目以获取更新通知！**
