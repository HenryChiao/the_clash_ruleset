# The Location Rule-Set

Location-based routing rules - Specialized rules for Wi-Fi Calling & Banking Services

[English](./README_EN.md) | [简体中文](./README.md)

---

## 📋 Rule List

### 🍎 Apple Services
| Filename | Description | Rules | Updated |
|----------|-------------|-------|---------|
| `apple-location.list` | Apple location detection service | 1 | 2026-01-05 |

---

### 📱 Wi-Fi Calling Rules

#### Americas

| Filename | Countries | Major Carriers | Rules |
|----------|-----------|----------------|-------|
| `wificalling-us.list` | 🇺🇸 USA | AT&T<br>T-Mobile<br>Ultra Mobile<br>Helium Mobile | 26 |
| `wificalling-americas.list` | 🇲🇽 Mexico | WIM | 1 |

#### Europe

| Filename | Countries | Major Carriers | Rules |
|----------|-----------|----------------|-------|
| `wificalling-uk.list` | 🇬🇧 UK | Vodafone UK<br>EE (CMLink UK)<br>Giffgaff<br>3UK<br>VOXI<br>CTEXCEL | 35 |
| `wificalling-de.list` | 🇩🇪 Germany | Vodafone DE<br>O2<br>E-Plus<br>Drillisch (1&1) | 27 |
| `wificalling-europe.list` | 🇳🇱 Netherlands<br>🇫🇮 Finland<br>🇮🇸 Iceland<br>🇱🇹 Lithuania<br>🇺🇦 Ukraine | Vodafone NL<br>Elisa<br>Nova<br>Pildyk<br>lifecell | 10 |

#### Asia-Pacific

| Filename | Countries | Major Carriers | Rules |
|----------|-----------|----------------|-------|
| `wificalling-hk.list` | 🇭🇰 Hong Kong | 3HK (Three)<br>CSL<br>HKT / 1010 / One2Free | 17 |
| `wificalling-asia.list` | 🇹🇭 Thailand<br>🇲🇾 Malaysia<br>🇱🇰 Sri Lanka | AIS<br>Maxis<br>Digi<br>Dialog | 7 |
| `wificalling-oceania.list` | 🇦🇺 Australia<br>🇳🇿 New Zealand | ALDI<br>Optus<br>Vodafone AU<br>One NZ<br>2degrees<br>Spark | 9 |

---

### 🏦 Banking Services Rules

| Filename | Region | Institutions | Rules |
|----------|--------|--------------|-------|
| `bank-hk.list` | 🇭🇰 Hong Kong | **Traditional Banks (13)**<br>HSBC, Hang Seng, BOC HK, BEA, SC<br>Citi, DBS, ICBC Asia, CCB Asia<br>OCBC, Dah Sing<br><br>**Virtual Banks (4)**<br>ZA Bank, WeLab Bank<br>Fusion Bank, Mox Bank | 20 |
| `bank-us.list` | 🇺🇸 USA | **Major Banks (10)**<br>JPMorgan Chase, Bank of America<br>Wells Fargo, U.S. Bank<br>Capital One, PNC, Truist<br>USAA, Navy Federal, Citi<br><br>**Credit Cards (1)**<br>American Express | 18 |

---

## 🚀 Usage

### Mihomo / Clash Meta Configuration

#### Method 1: Rule Providers (Recommended)

```yaml
rule-providers:
  # Wi-Fi Calling - USA
  wificalling-us:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/wificalling-us.list"
    path: ./ruleset/wificalling-us.yaml
    interval: 86400

  # Wi-Fi Calling - Hong Kong
  wificalling-hk:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/wificalling-hk.list"
    path: ./ruleset/wificalling-hk.yaml
    interval: 86400

  # Hong Kong Banks
  bank-hk:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/HenryChiao/the_clash_ruleset/main/The_Location_rule-set/bank-hk.list"
    path: ./ruleset/bank-hk.yaml
    interval: 86400

proxy-groups:
  - name: "🇺🇸 US"
    type: select
    # Your US proxies

  - name: "🇭🇰 HK"
    type: select
    # Your HK proxies

rules:
  - RULE-SET,wificalling-us,🇺🇸 US
  - RULE-SET,wificalling-hk,🇭🇰 HK
  - RULE-SET,bank-hk,🇭🇰 HK
```

#### Method 2: CDN Acceleration (Recommended for China)

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

## 💡 Configuration Guidelines

### ⚠️ IMPORTANT: Wi-Fi Calling Configuration

**Wi-Fi Calling should use proxies in the corresponding country, NOT direct connection!**

```yaml
# ✅ Correct Configuration
rules:
  - RULE-SET,wificalling-us,🇺🇸 US Proxy
  - RULE-SET,wificalling-uk,🇬🇧 UK Proxy
  - RULE-SET,wificalling-hk,🇭🇰 HK Proxy
  - RULE-SET,wificalling-de,🇩🇪 DE Proxy

# ❌ Wrong Configuration
rules:
  - RULE-SET,wificalling-us,DIRECT  # Wrong!
  - RULE-SET,wificalling-uk,DIRECT  # Wrong!
```

#### Why can't use DIRECT?

1. **Geographic Location Verification**
   - Wi-Fi Calling services need to connect to the carrier's ePDG (evolved Packet Data Gateway) servers in the corresponding country
   - Carriers verify the geographic location of the connection source
   - Direct connections will be rejected if you're not in the carrier's country

2. **IP Address Restrictions**
   - Carrier ePDG servers typically only accept connections from specific regions
   - Using a proxy in the corresponding region makes your connection appear to come from the correct location

3. **Service Availability**
   - Some carriers' Wi-Fi Calling services are only available domestically
   - Using proxies can bypass geographic restrictions

#### Real-world Scenarios

**Scenario A: Using US T-Mobile Wi-Fi Calling from China**
```yaml
# Need to use US proxy
- RULE-SET,wificalling-us,🇺🇸 US Proxy
```

**Scenario B: Using HK 3HK Wi-Fi Calling from UK**
```yaml
# Need to use HK proxy
- RULE-SET,wificalling-hk,🇭🇰 HK Proxy
```

**Scenario C: Already in the carrier's country**
```yaml
# If you're already in the US, you can use direct
- RULE-SET,wificalling-us,DIRECT

# But for stability, still recommend using local proxy
- RULE-SET,wificalling-us,🇺🇸 US Proxy
```

---

### Banking Services Configuration

#### Option A: Use Region-specific Proxies (Recommended)

```yaml
rules:
  - RULE-SET,bank-hk,🇭🇰 HK Proxy
  - RULE-SET,bank-us,🇺🇸 US Proxy
```

**Advantages:**
- ✅ Bypass geographic restrictions
- ✅ Better access speed (especially when abroad)
- ✅ Avoid cross-border access timeouts

**Use Cases:**
- Accessing HK/US banks from abroad
- Banks with geographic access restrictions
- Need faster access speeds

#### Option B: Direct Connection

```yaml
rules:
  - RULE-SET,bank-hk,DIRECT
  - RULE-SET,bank-us,DIRECT
```

**Advantages:**
- ✅ Lowest latency
- ✅ Avoid proxy instability
- ✅ Lower risk of triggering fraud detection

**Use Cases:**
- Already in the bank's region
- Stable network environment
- No geographic restrictions

---

## 📊 Rule Details

### Wi-Fi Calling Rule Components

Each Wi-Fi Calling rule file contains:

1. **Domain Rules (DOMAIN-SUFFIX)**
   - ePDG server domains
   - IMS core network domains
   - Carrier-related domains

2. **IP Range Rules (IP-CIDR)**
   - Carrier ePDG server IP ranges
   - Uses `no-resolve` to prevent DNS leaks

3. **Keyword Rules (DOMAIN-KEYWORD)**
   - Carrier brand keywords (e.g., t-mobile)

### Banking Rule Components

Each banking rule file contains:

1. **Main Domains**
   - Official website domains
   - Mobile app domains

2. **API Domains**
   - Service API domains
   - Online banking domains

3. **Related Services**
   - Customer service domains
   - Payment gateway domains

---

## 🔍 MCC/MNC Code Reference

### What is MCC/MNC?

- **MCC (Mobile Country Code)**: 3-digit mobile country code
- **MNC (Mobile Network Code)**: 2-3 digit mobile network code
- Format: `epdg.epc.mncXXX.mccYYY.pub.3gppnetwork.org`

### Common MCC/MNC List

| MCC | Country | MNC | Carrier | Example Domain |
|-----|---------|-----|---------|----------------|
| 310 | 🇺🇸 USA | 260 | T-Mobile | epdg.epc.mnc260.mcc310.pub.3gppnetwork.org |
| 234 | 🇬🇧 UK | 015 | Vodafone UK | epdg.epc.mnc015.mcc234.pub.3gppnetwork.org |
| 234 | 🇬🇧 UK | 010 | O2 (Giffgaff) | epdg.epc.mnc010.mcc234.pub.3gppnetwork.org |
| 454 | 🇭🇰 HK | 000 | 3HK | epdg.epc.mnc000.mcc454.pub.3gppnetwork.org |
| 262 | 🇩🇪 DE | 002 | Vodafone DE | epdg.epc.mnc002.mcc262.pub.3gppnetwork.org |
| 520 | 🇹🇭 TH | 003 | AIS | epdg.epc.mnc003.mcc520.pub.3gppnetwork.org |
| 505 | 🇦🇺 AU | 003 | Vodafone AU | epdg.epc.mnc003.mcc505.pub.3gppnetwork.org |
| 530 | 🇳🇿 NZ | 001 | One NZ | epdg.epc.mnc001.mcc530.pub.3gppnetwork.org |

See rule file comments for complete list.

---

## 🔧 Troubleshooting

### Wi-Fi Calling Connection Issues

#### Issue 1: "Cannot connect to Wi-Fi Calling"

**Possible Causes:**
- ❌ Rules configured as DIRECT instead of region-specific proxy
- ❌ Poor proxy quality, high latency
- ❌ Proxy IP blocked by carrier

**Solutions:**
1. Confirm using region-specific proxy
   ```yaml
   - RULE-SET,wificalling-us,🇺🇸 US Proxy  # ✅
   - RULE-SET,wificalling-us,DIRECT         # ❌
   ```

2. Check proxy latency
   - Recommend latency < 200ms
   - Use stable native IP proxies

3. Try different proxies

#### Issue 2: Frequent disconnections

**Possible Causes:**
- Unstable proxy
- Insufficient bandwidth
- IP restrictions

**Solutions:**
1. Use high-quality proxies
2. Avoid shared IP proxies
3. Contact proxy provider

#### Issue 3: Rules not working

**Possible Causes:**
- Rule loading failed
- Incorrect rule priority
- Cache issues

**Solutions:**
```bash
# 1. Check if rules are loaded
cat /path/to/mihomo/ruleset/wificalling-us.yaml

# 2. Clear cache
rm -rf /path/to/mihomo/ruleset/*.yaml

# 3. Restart Mihomo
systemctl restart mihomo

# 4. Check logs
tail -f /var/log/mihomo/mihomo.log
```

### Banking App Login Issues

#### Issue 1: "Network Error"

**Solutions:**
1. Try switching strategies
   - Using proxy → Try direct
   - Using direct → Try proxy

2. Check for missing domains
   - Use packet capture tools
   - Add missing domains to rules

#### Issue 2: Fraud detection triggered

**Causes:**
- Frequent IP changes
- Using unusual region IPs

**Solutions:**
1. Use fixed proxies
2. Avoid frequent proxy switching
3. Contact bank if necessary

---

## 📝 Changelog

### 2026-01-05
- ✅ Initial release
- ✅ Coverage: 15 countries/regions
- ✅ Support: 40+ carriers
- ✅ Include: 31 banks

### Future Updates
- 🔄 Regular rule validation
- 🔄 Add more countries and carriers
- 🔄 Performance optimization

---

## 🤝 Contributing

### Adding New Carriers

To add new carrier rules, please provide:

1. **Basic Information**
   - Carrier name
   - Country/region
   - MCC/MNC codes

2. **Technical Information**
   - ePDG domain (format: `epdg.epc.mncXXX.mccYYY.pub.3gppnetwork.org`)
   - IP address ranges
   - Related domains

3. **Testing Verification**
   - Test screenshots
   - Connection logs
   - Testing environment details

### Reporting Issues

Please report on [GitHub Issues](https://github.com/HenryChiao/the_clash_ruleset/issues):

- Rule failures
- New carrier requests
- Bugs and suggestions

---

## 📚 References

### Wi-Fi Calling Technical Documentation
- [3GPP ePDG Specifications](https://www.3gpp.org/)
- [IMS/VoLTE Technical Whitepaper](https://www.gsma.com/)

### Mihomo Configuration Documentation
- [Mihomo Wiki](https://wiki.metacubex.one/)
- [Rule Providers Documentation](https://wiki.metacubex.one/config/rule-providers/)

### MCC/MNC Lookup
- [MCC-MNC Database](https://www.mcc-mnc.com/)
- [ITU Official List](https://www.itu.int/)

---

## ⚠️ Disclaimer

- This ruleset is for educational purposes only
- Test thoroughly before use
- Carriers may change server configurations at any time
- Users assume all risks
- Comply with local laws and carrier terms of service

---

## 📞 Support

For issues, please contact via:

- 📧 GitHub Issues: [Submit Issue](https://github.com/HenryChiao/the_clash_ruleset/issues)
- 💬 Discussions: [Join Discussion](https://github.com/HenryChiao/the_clash_ruleset/discussions)

---

<div align="center">

**Last Updated**: January 7, 2026

Made with ❤️ by [HenryChiao](https://github.com/HenryChiao)

[Back to Main](../README.md)

</div>
