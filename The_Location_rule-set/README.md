# Wi-Fi Calling & 银行规则集 - 使用说明

## 📦 规则文件列表

### 🍎 Apple 通用
- `apple-location.list` - Apple 地区检测服务

### 📱 Wi-Fi Calling 规则

#### 美洲地区
- `wificalling-us.list` - 美国 (AT&T, T-Mobile, Ultra, Helium)
- `wificalling-americas.list` - 墨西哥 (WIM)

#### 欧洲地区
- `wificalling-uk.list` - 英国 (Vodafone, EE, Giffgaff, 3UK, VOXI, CTEXCEL)
- `wificalling-de.list` - 德国 (Vodafone, O2, E-Plus, 1&1)
- `wificalling-europe.list` - 其他欧洲国家 (荷兰, 芬兰, 冰岛, 立陶宛, 乌克兰)

#### 亚太地区
- `wificalling-hk.list` - 香港 (3HK, CSL, HKT)
- `wificalling-asia.list` - 泰国, 马来西亚, 斯里兰卡
- `wificalling-oceania.list` - 澳大利亚 & 新西兰

### 🏦 银行规则
- `bank-hk.list` - 香港银行 (13家传统银行 + 4家虚拟银行)
- `bank-us.list` - 美国银行 (10家主要银行 + 美国运通)

---

## 📊 规则统计

| 类别 | 文件数 | 规则总数 | 覆盖范围 |
|------|--------|----------|----------|
| Apple | 1 | 1 | 全球 |
| Wi-Fi Calling | 7 | 160+ | 15国/地区, 40+运营商 |
| 银行 | 2 | 42 | 香港, 美国 |
| **总计** | **10** | **200+** | **全球主要地区** |

---

## 🚀 快速开始

### 方案一: 使用 Rule Providers (推荐)

1. **上传规则文件**
   - 将所有 `.list` 文件上传到 GitHub 仓库或 CDN
   - 确保文件可通过 HTTPS 访问

2. **配置 Mihomo**
   ```yaml
   rule-providers:
     wificalling-us:
       type: http
       behavior: classical
       url: "https://raw.githubusercontent.com/your-repo/wificalling-us.list"
       path: ./ruleset/wificalling-us.yaml
       interval: 86400
   
   rules:
     - RULE-SET,wificalling-us,DIRECT
   ```

3. **重新加载配置**
   ```bash
   # 重启 Mihomo 或重新加载配置
   systemctl restart mihomo
   ```

### 方案二: 直接内嵌规则

将规则内容直接复制到 Mihomo 配置文件的 `rules` 部分:

```yaml
rules:
  # 美国 Wi-Fi Calling
  - DOMAIN-SUFFIX,epdg.epc.att.net,DIRECT
  - DOMAIN-SUFFIX,crl.t-mobile.com,DIRECT
  - IP-CIDR,107.122.31.0/32,DIRECT,no-resolve
  
  # 香港银行
  - DOMAIN-SUFFIX,hsbc.com.hk,HK-Proxy
  - DOMAIN-SUFFIX,hangseng.com,HK-Proxy
```

---

## 📋 各地区运营商覆盖

### 🇺🇸 美国
- **AT&T** - 完整支持
- **T-Mobile** - 完整支持 (含 Ultra Mobile, Helium Mobile)

### 🇬🇧 英国
- **Vodafone UK** - 完整支持
- **EE** - 完整支持 (CMLink UK)
- **Giffgaff** - 完整支持 (使用O2网络)
- **3UK** - 完整支持
- **VOXI** - 完整支持
- **CTEXCEL** - 完整支持

### 🇭🇰 香港
- **3HK** (Three Hong Kong) - 完整支持
- **CSL** - 完整支持
- **HKT/1010/One2Free** - 完整支持

### 🇩🇪 德国
- **Vodafone DE** - 完整支持
- **O2** - 完整支持
- **E-Plus** - 完整支持
- **1&1 (Drillisch)** - 完整支持

### 🇦🇺 澳大利亚
- **ALDI** - 完整支持
- **Optus** - 完整支持 (felix)
- **Vodafone AU** - 完整支持 (amaysim)

### 🇳🇿 新西兰
- **One NZ** - 完整支持
- **2degrees** - 完整支持
- **Spark/Skinny** - 完整支持

### 🇹🇭 泰国
- **AIS** - 完整支持

### 🇲🇾 马来西亚
- **Maxis** - 完整支持
- **Digi** - 完整支持

### 其他地区
- 🇳🇱 荷兰: Vodafone NL
- 🇫🇮 芬兰: Elisa
- 🇮🇸 冰岛: Nova
- 🇱🇹 立陶宛: Pildyk
- 🇺🇦 乌克兰: lifecell
- 🇱🇰 斯里兰卡: Dialog
- 🇲🇽 墨西哥: WIM

---

## 💡 配置建议

### Wi-Fi Calling 策略

**推荐配置: 全部 DIRECT 直连**

```yaml
proxy-groups:
  - name: "📱 Wi-Fi Calling"
    type: select
    proxies:
      - DIRECT

rules:
  - RULE-SET,wificalling-us,📱 Wi-Fi Calling
  - RULE-SET,wificalling-uk,📱 Wi-Fi Calling
  - RULE-SET,wificalling-hk,📱 Wi-Fi Calling
  # ... 其他地区规则
```

**原因:**
- Wi-Fi Calling 需要低延迟连接运营商 ePDG 网关
- 通过代理会增加延迟,影响通话质量
- 某些运营商可能检测代理连接并拒绝服务

### 银行规则策略

#### 方案 A: 使用对应地区节点 (推荐)

```yaml
proxy-groups:
  - name: "🏦 香港银行"
    type: select
    proxies:
      - 🇭🇰 香港节点
      - DIRECT

  - name: "🏦 美国银行"
    type: select
    proxies:
      - 🇺🇸 美国节点
      - DIRECT

rules:
  - RULE-SET,bank-hk,🏦 香港银行
  - RULE-SET,bank-us,🏦 美国银行
```

**适用场景:**
- 在非银行所在地区访问银行服务
- 需要绕过地区限制
- 提升访问速度

#### 方案 B: 全部直连

```yaml
rules:
  - RULE-SET,bank-hk,DIRECT
  - RULE-SET,bank-us,DIRECT
```

**适用场景:**
- 在银行所在地区使用
- 追求最低延迟
- 避免代理连接触发风控

---

## ⚙️ 规则优先级

推荐规则顺序 (从高到低):

```yaml
rules:
  # 1. Apple 服务
  - RULE-SET,apple-location,DIRECT
  
  # 2. Wi-Fi Calling (最高优先级)
  - RULE-SET,wificalling-us,DIRECT
  - RULE-SET,wificalling-uk,DIRECT
  - RULE-SET,wificalling-hk,DIRECT
  - RULE-SET,wificalling-de,DIRECT
  - RULE-SET,wificalling-asia,DIRECT
  - RULE-SET,wificalling-oceania,DIRECT
  - RULE-SET,wificalling-europe-other,DIRECT
  - RULE-SET,wificalling-mexico,DIRECT
  
  # 3. 银行服务
  - RULE-SET,bank-hk,🏦 香港银行
  - RULE-SET,bank-us,🏦 美国银行
  
  # 4. 其他规则...
  - RULE-SET,your-other-rules,PROXY
  
  # 5. 最终匹配
  - MATCH,DIRECT
```

---

## 🔧 故障排查

### Wi-Fi Calling 无法连接

1. **检查规则是否生效**
   ```bash
   # 查看 Mihomo 日志
   tail -f /var/log/mihomo/mihomo.log
   ```

2. **确认规则匹配**
   - 在日志中搜索 ePDG 相关域名
   - 确认流量走的是 DIRECT 而非代理

3. **验证 DNS 解析**
   ```bash
   # 测试域名解析
   nslookup epdg.epc.att.net
   ```

4. **检查 IP 规则**
   - 确保所有 IP-CIDR 规则都包含 `no-resolve`
   - 避免 DNS 泄露

### 银行应用无法登录

1. **尝试切换策略**
   - 如果用的代理,尝试切换为 DIRECT
   - 如果用的 DIRECT,尝试切换为对应地区节点

2. **检查额外域名**
   - 某些银行可能有额外的 API 域名
   - 使用抓包工具 (如 Charles) 查找缺失的域名

3. **排除风控影响**
   - 频繁切换 IP 可能触发银行风控
   - 建议使用固定节点或直连

### 规则更新失败

1. **检查文件 URL**
   - 确认 URL 可以通过浏览器访问
   - 检查是否使用 HTTPS 协议

2. **验证文件格式**
   - 确保文件是 UTF-8 编码
   - 检查是否有语法错误

3. **清除缓存**
   ```bash
   # 删除缓存文件
   rm -rf /path/to/mihomo/ruleset/*.yaml
   # 重启 Mihomo
   systemctl restart mihomo
   ```

---

## 📝 自定义规则

### 添加新的运营商

1. **确定 MCC/MNC 代码**
   - MCC: 移动国家代码
   - MNC: 移动网络代码

2. **查找 ePDG 域名**
   - 格式通常为: `epdg.epc.mncXXX.mccYYY.pub.3gppnetwork.org`
   - 例如: `epdg.epc.mnc015.mcc234.pub.3gppnetwork.org` (Vodafone UK)

3. **添加到对应规则文件**
   ```
   # 新运营商
   DOMAIN-SUFFIX,epdg.epc.mncXXX.mccYYY.pub.3gppnetwork.org
   IP-CIDR,xxx.xxx.xxx.xxx/xx,no-resolve
   ```

### 添加新的银行

```
# 新银行
DOMAIN-SUFFIX,newbank.com
DOMAIN-SUFFIX,api.newbank.com
DOMAIN-SUFFIX,m.newbank.com
```

---

## 🔄 更新日志

### 2026-01-05
- ✅ 初始版本发布
- ✅ 覆盖 15 个国家/地区
- ✅ 支持 40+ 运营商
- ✅ 包含 25+ 家银行

---

## 📞 支持与反馈

### 报告问题
- 如果发现规则失效或需要添加新运营商
- 请提供详细的运营商信息和测试结果

### 贡献规则
- 欢迎提交 Pull Request
- 请确保规则经过实际测试验证

---

## 📄 许可证

本规则集遵循 MIT 许可证开源

---

## ⚠️ 免责声明

- 这些规则仅供参考,使用前请自行测试
- 运营商可能随时更改 ePDG 服务器地址
- 作者不对使用这些规则造成的任何问题负责
- 请遵守当地法律法规和运营商服务条款

---

**最后更新时间**: 2026年1月5日
