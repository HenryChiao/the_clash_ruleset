# The Location Rule-Set

地区分流规则集 - Wi-Fi Calling & 银行服务专用规则

---

## 📋 规则列表

### 🍎 Apple 服务
| 文件名 | 说明 | 规则数 | 更新日期 |
|--------|------|--------|----------|
| `apple-location.list` | Apple 地区检测服务 | 1 | 2026-01-05 |

---

### 📱 Wi-Fi Calling 规则

#### 美洲地区

| 文件名 | 覆盖国家 | 主要运营商 | 规则数 |
|--------|----------|-----------|--------|
| `wificalling-us.list` | 🇺🇸 美国 | AT&T<br>T-Mobile<br>Ultra Mobile<br>Helium Mobile | 26 |
| `wificalling-americas.list` | 🇲🇽 墨西哥 | WIM | 1 |

#### 欧洲地区

| 文件名 | 覆盖国家 | 主要运营商 | 规则数 |
|--------|----------|-----------|--------|
| `wificalling-uk.list` | 🇬🇧 英国 | Vodafone UK<br>EE (CMLink UK)<br>Giffgaff<br>3UK<br>VOXI<br>CTEXCEL | 35 |
| `wificalling-de.list` | 🇩🇪 德国 | Vodafone DE<br>O2<br>E-Plus<br>Drillisch (1&1) | 27 |
| `wificalling-europe.list` | 🇳🇱 荷兰<br>🇫🇮 芬兰<br>🇮🇸 冰岛<br>🇱🇹 立陶宛<br>🇺🇦 乌克兰 | Vodafone NL<br>Elisa<br>Nova<br>Pildyk<br>lifecell | 10 |

#### 亚太地区

| 文件名 | 覆盖国家 | 主要运营商 | 规则数 |
|--------|----------|-----------|--------|
| `wificalling-hk.list` | 🇭🇰 香港 | 3HK (Three)<br>CSL<br>HKT / 1010 / One2Free | 17 |
| `wificalling-asia.list` | 🇹🇭 泰国<br>🇲🇾 马来西亚<br>🇱🇰 斯里兰卡 | AIS<br>Maxis<br>Digi<br>Dialog | 7 |
| `wificalling-oceania.list` | 🇦🇺 澳大利亚<br>🇳🇿 新西兰 | ALDI<br>Optus<br>Vodafone AU<br>One NZ<br>2degrees<br>Spark | 9 |

---

### 🏦 银行服务规则

| 文件名 | 覆盖地区 | 包含机构 | 规则数 |
|--------|----------|----------|--------|
| `bank-hk.list` | 🇭🇰 香港 | **传统银行 (13家)**<br>汇丰、恒生、中银香港、东亚、渣打<br>花旗、星展、工银亚洲、建行亚洲<br>华侨银行、大新银行<br><br>**虚拟银行 (4家)**<br>ZA Bank、WeLab Bank<br>Fusion Bank、Mox Bank | 20 |
| `bank-us.list` | 🇺🇸 美国 | **主要银行 (10家)**<br>JPMorgan Chase、Bank of America<br>Wells Fargo、U.S. Bank<br>Capital One、PNC、Truist<br>USAA、Navy Federal、Citi<br><br>**信用卡 (1家)**<br>American Express | 18 |

---

## 🚀 使用方法

### Mihomo / Clash Meta 配置

#### 方式一: Rule Providers (推荐)

```yaml
rule-providers:
  # Wi-Fi Calling - 美国
  wificalling-us:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/wificalling-us.list"
    path: ./ruleset/wificalling-us.yaml
    interval: 86400

  # Wi-Fi Calling - 香港
  wificalling-hk:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/wificalling-hk.list"
    path: ./ruleset/wificalling-hk.yaml
    interval: 86400

  # 香港银行
  bank-hk:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/bank-hk.list"
    path: ./ruleset/bank-hk.yaml
    interval: 86400

proxy-groups:
  - name: "🇺🇸 美国"
    type: select
    # 你的美国节点

  - name: "🇭🇰 香港"
    type: select
    # 你的香港节点

rules:
  - RULE-SET,wificalling-us,🇺🇸 美国
  - RULE-SET,wificalling-hk,🇭🇰 香港
  - RULE-SET,bank-hk,🇭🇰 香港
```

#### 方式二: CDN 加速 (国内推荐)

```yaml
rule-providers:
  wificalling-us:
    type: http
    behavior: classical
    url: "https://cdn.jsdelivr.net/gh/HenryChiao/the_clash_ruleset@main/The_Location_rule-set/wificalling-us.list"
    path: ./ruleset/wificalling-us.yaml
    interval: 86400
```

---

## 💡 配置建议

### ⚠️ 重要: Wi-Fi Calling 策略配置

**Wi-Fi Calling 应该使用对应国家的节点，而不是直连！**

```yaml
# ✅ 正确配置
rules:
  - RULE-SET,wificalling-us,🇺🇸 美国节点
  - RULE-SET,wificalling-uk,🇬🇧 英国节点
  - RULE-SET,wificalling-hk,🇭🇰 香港节点
  - RULE-SET,wificalling-de,🇩🇪 德国节点

# ❌ 错误配置
rules:
  - RULE-SET,wificalling-us,DIRECT  # 错误!
  - RULE-SET,wificalling-uk,DIRECT  # 错误!
```

#### 为什么不能直连？

1. **地理位置验证**
   - Wi-Fi Calling 服务需要连接到运营商在对应国家的 ePDG (evolved Packet Data Gateway) 服务器
   - 运营商会验证连接来源的地理位置
   - 如果您不在运营商所在国家，直连会被拒绝

2. **IP 地址限制**
   - 运营商的 ePDG 服务器通常只接受来自特定地区的连接
   - 使用对应地区节点可以让您的连接看起来来自正确的位置

3. **服务可用性**
   - 某些运营商的 Wi-Fi Calling 服务仅在本国境内提供
   - 使用节点可以绕过地理限制

#### 实际使用场景

**场景 A: 在中国大陆使用美国 T-Mobile 的 Wi-Fi Calling**
```yaml
# 需要使用美国节点
- RULE-SET,wificalling-us,🇺🇸 美国节点
```

**场景 B: 在英国使用香港 3HK 的 Wi-Fi Calling**
```yaml
# 需要使用香港节点
- RULE-SET,wificalling-hk,🇭🇰 香港节点
```

**场景 C: 已在运营商所在国家**
```yaml
# 如果您已经在美国，可以直连
- RULE-SET,wificalling-us,DIRECT

# 但为了稳定性，仍建议使用本地节点
- RULE-SET,wificalling-us,🇺🇸 美国节点
```

---

### 银行服务策略配置

#### 方案 A: 使用对应地区节点 (推荐)

```yaml
rules:
  - RULE-SET,bank-hk,🇭🇰 香港节点
  - RULE-SET,bank-us,🇺🇸 美国节点
```

**优点:**
- ✅ 绕过地理位置限制
- ✅ 提升访问速度（特别是在国外时）
- ✅ 避免跨境访问导致的超时

**适用场景:**
- 在国外访问香港/美国银行
- 银行有地区访问限制
- 需要更快的访问速度

#### 方案 B: 直连

```yaml
rules:
  - RULE-SET,bank-hk,DIRECT
  - RULE-SET,bank-us,DIRECT
```

**优点:**
- ✅ 最低延迟
- ✅ 避免节点不稳定
- ✅ 降低触发风控的风险

**适用场景:**
- 已在银行所在地区
- 网络环境稳定
- 银行无地理位置限制

---

## 📊 规则详情

### Wi-Fi Calling 规则组成

每个 Wi-Fi Calling 规则文件包含:

1. **域名规则 (DOMAIN-SUFFIX)**
   - ePDG 服务器域名
   - IMS 核心网域名
   - 运营商相关域名

2. **IP 段规则 (IP-CIDR)**
   - 运营商 ePDG 服务器 IP 段
   - 使用 `no-resolve` 避免 DNS 泄露

3. **关键字规则 (DOMAIN-KEYWORD)**
   - 运营商品牌关键字 (如 t-mobile)

### 银行规则组成

每个银行规则文件包含:

1. **主域名**
   - 官方网站域名
   - 移动端域名

2. **API 域名**
   - 接口服务域名
   - 在线银行域名

3. **相关服务**
   - 客户服务域名
   - 支付网关域名

---

## 🔍 运营商 MCC/MNC 代码参考

### 什么是 MCC/MNC?

- **MCC (Mobile Country Code)**: 移动国家代码，3位数字
- **MNC (Mobile Network Code)**: 移动网络代码，2-3位数字
- 格式: `epdg.epc.mncXXX.mccYYY.pub.3gppnetwork.org`

### 常用 MCC/MNC 列表

| MCC | 国家 | MNC | 运营商 | 示例域名 |
|-----|------|-----|--------|---------|
| 310 | 🇺🇸 美国 | 260 | T-Mobile | epdg.epc.mnc260.mcc310.pub.3gppnetwork.org |
| 234 | 🇬🇧 英国 | 015 | Vodafone UK | epdg.epc.mnc015.mcc234.pub.3gppnetwork.org |
| 234 | 🇬🇧 英国 | 010 | O2 (Giffgaff) | epdg.epc.mnc010.mcc234.pub.3gppnetwork.org |
| 454 | 🇭🇰 香港 | 000 | 3HK | epdg.epc.mnc000.mcc454.pub.3gppnetwork.org |
| 262 | 🇩🇪 德国 | 002 | Vodafone DE | epdg.epc.mnc002.mcc262.pub.3gppnetwork.org |
| 520 | 🇹🇭 泰国 | 003 | AIS | epdg.epc.mnc003.mcc520.pub.3gppnetwork.org |
| 505 | 🇦🇺 澳洲 | 003 | Vodafone AU | epdg.epc.mnc003.mcc505.pub.3gppnetwork.org |
| 530 | 🇳🇿 新西兰 | 001 | One NZ | epdg.epc.mnc001.mcc530.pub.3gppnetwork.org |

完整列表请参考各规则文件注释。

---

## 🔧 故障排查

### Wi-Fi Calling 无法连接

#### 问题 1: 显示"无法连接到 Wi-Fi Calling"

**可能原因:**
- ❌ 规则配置为 DIRECT 而非对应地区节点
- ❌ 节点质量差，延迟过高
- ❌ 节点被运营商封禁

**解决方案:**
1. 确认使用对应地区节点
   ```yaml
   - RULE-SET,wificalling-us,🇺🇸 美国节点  # ✅
   - RULE-SET,wificalling-us,DIRECT         # ❌
   ```

2. 检查节点延迟
   - 建议延迟 < 200ms
   - 使用稳定的原生 IP 节点

3. 更换节点测试

#### 问题 2: 连接后频繁断线

**可能原因:**
- 节点不稳定
- 带宽不足
- 节点 IP 被限制

**解决方案:**
1. 使用高质量节点
2. 避免共享 IP 节点
3. 联系节点提供商

#### 问题 3: 规则没有生效

**可能原因:**
- 规则加载失败
- 规则优先级错误
- 缓存问题

**解决方案:**
```bash
# 1. 检查规则是否加载
cat /path/to/mihomo/ruleset/wificalling-us.yaml

# 2. 清除缓存
rm -rf /path/to/mihomo/ruleset/*.yaml

# 3. 重启 Mihomo
systemctl restart mihomo

# 4. 查看日志
tail -f /var/log/mihomo/mihomo.log
```

### 银行应用无法登录

#### 问题 1: 提示"网络异常"

**解决方案:**
1. 尝试切换策略
   - 使用节点 → 尝试直连
   - 使用直连 → 尝试节点

2. 检查是否有额外域名
   - 使用抓包工具查看请求
   - 添加缺失的域名到规则

#### 问题 2: 触发风控验证

**原因:**
- 频繁切换 IP 地址
- 使用异常地区 IP

**解决方案:**
1. 使用固定节点
2. 避免频繁切换代理
3. 必要时联系银行客服

---

## 📝 规则更新日志

### 2026-01-05
- ✅ 初始版本发布
- ✅ 覆盖 15 个国家/地区
- ✅ 支持 40+ 运营商
- ✅ 包含 31 家银行

### 后续更新计划
- 🔄 定期验证规则有效性
- 🔄 添加更多国家和运营商
- 🔄 优化规则性能

---

## 🤝 贡献指南

### 添加新运营商

如果您想添加新的运营商规则，请提供:

1. **基本信息**
   - 运营商名称
   - 所属国家/地区
   - MCC/MNC 代码

2. **技术信息**
   - ePDG 域名 (格式: `epdg.epc.mncXXX.mccYYY.pub.3gppnetwork.org`)
   - IP 地址段
   - 相关域名

3. **测试验证**
   - 实际测试截图
   - 连接日志
   - 测试环境说明

### 报告问题

请在 [GitHub Issues](https://github.com/HenryChiao/the_clash_ruleset/issues) 中报告:

- 规则失效
- 新运营商需求
- 错误和建议

---

## 📚 参考资料

### Wi-Fi Calling 技术文档
- [3GPP ePDG 规范](https://www.3gpp.org/)
- [IMS/VoLTE 技术白皮书](https://www.gsma.com/)

### Mihomo 配置文档
- [Mihomo Wiki](https://wiki.metacubex.one/)
- [Rule Providers 文档](https://wiki.metacubex.one/config/rule-providers/)

### MCC/MNC 查询
- [MCC-MNC 数据库](https://www.mcc-mnc.com/)
- [ITU 官方列表](https://www.itu.int/)

---

## ⚠️ 免责声明

- 本规则集仅供学习研究使用
- 使用前请自行测试验证
- 运营商可能随时更改服务器配置
- 使用者需自行承担使用风险
- 请遵守当地法律法规和运营商服务条款

---

## 📞 技术支持

如有问题，请通过以下方式联系:

- 📧 GitHub Issues: [提交问题](https://github.com/HenryChiao/the_clash_ruleset/issues)
- 💬 Discussions: [参与讨论](https://github.com/HenryChiao/the_clash_ruleset/discussions)

---

<div align="center">

**最后更新时间**: 2026年1月7日

Made with ❤️ by [HenryChiao](https://github.com/HenryChiao)

[返回主页](../README.md)

</div>
