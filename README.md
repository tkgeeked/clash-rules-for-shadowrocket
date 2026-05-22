# Clash Rules for Shadowrocket

将 [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules) 项目转换为 **Shadowrocket** 格式的规则集，支持**每日自动更新**。

## ✨ 特点

- **🔄 自动更新**：GitHub Actions 每天北京时间 06:30 自动同步最新规则
- **📱 Shadowrocket 专用**：规则格式专为 Shadowrocket 优化
- **双模式支持**：提供白名单和黑名单两种模式
- **🚫 广告拦截**：171,774 条广告域名拦截规则
- **🌐 GFW 列表**：4,243 条需代理的域名
- **🍎 智能分流**：Apple、iCloud、Google 智能直连
- **📍 IP/CIDR 规则**：中国 IP 直连 + Telegram IP 代理

## 📦 规则集列表

### 1. 白名单模式（推荐）

**订阅 URL**：
```
https://raw.githubusercontent.com/tkgeeked/clash-rules-for-shadowrocket/main/loyalsoldier-whitelist.conf
```

**特点**：未命中规则的流量默认走代理。适合线路稳定、不缺流量的用户。

### 2. 黑名单模式

**订阅 URL**：
```
https://raw.githubusercontent.com/tkgeeked/clash-rules-for-shadowrocket/main/loyalsoldier-blacklist.conf
```

**特点**：只有命中规则的流量才走代理，其他全部直连。适合流量有限或线路不稳定的用户。

## 📊 规则结构

| 规则类型 | 数量 | 白名单模式 | 黑名单模式 |
|---------|------|-----------|-----------|
| 广告拦截 | ~171,774 条 | REJECT-DROP | REJECT-DROP |
| 代理域名 | ~26,312 条 | PROXY | PROXY |
| 直连域名 | ~113,688 条 | DIRECT | DIRECT |
| GFW 列表 | ~4,243 条 | PROXY | PROXY |
| Apple | 164 条 | DIRECT | DIRECT |
| iCloud | 53 条 | DIRECT | DIRECT |
| Google | 113 条 | DIRECT | DIRECT |
| 非中国顶级域名 | 832 条 | PROXY | PROXY |
| Telegram IP | 13 条 | PROXY | PROXY |
| 中国 IP | ~5,675 条 | DIRECT | DIRECT |
| 局域网 IP | 19 条 | DIRECT | DIRECT |
| 应用直连 | 97 个 | DIRECT | DIRECT |
| GEOIP | 1 条 | DIRECT | DIRECT |
| **FINAL** | 1 条 | **PROXY** | **DIRECT** |

**总规则数**：~322,985 条  
**文件大小**：~14.6 MB

## 🎯 选择白名单还是黑名单？

### 白名单模式（推荐）

✅ **适合**：
- 线路稳定、速度快
- 不缺代理流量
- 希望所有流量都经过代理保护隐私

📝 **逻辑**：`FINAL,PROXY` - 没命中规则的流量都走代理

### 黑名单模式

✅ **适合**：
- 流量有限或线路不稳定
- 只需要特定网站走代理
- 软路由/家庭网关用户

📝 **逻辑**：`FINAL,DIRECT` - 没命中规则的流量都直连

## 📖 使用方法

### 1. 在 Shadowrocket 中导入

1. 打开 **Shadowrocket**
2. 进入「配置」页面
3. 点击「+」添加配置
4. 选择「添加订阅」或「从 URL 导入」
5. 粘贴上面的 URL（选一个即可）
6. 下载并启用该规则集

### 2. 启用规则

- 在 Shadowrocket 的「路由」设置中，启用导入的规则
- 推荐使用「规则模式」

## 🔄 自动更新

规则会**每天自动更新**，无需手动操作：

- **更新时间**：每天北京时间 06:30
- **更新来源**：[Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules)
- **更新机制**：自动从 clash-rules 下载所有规则文件，转换为 Shadowrocket 格式并推送

如果你想**立即更新规则**：
1. 访问 [GitHub Actions 页面](https://github.com/tkgeeked/clash-rules-for-shadowrocket/actions)
2. 点击 `Convert Loyalsoldier Rules to Shadowrocket` 工作流
3. 点击「Run workflow」手动触发
4. 等待几分钟，规则会自动同步并推送

## 📝 规则格式示例

### 白名单模式

```
[General]
update-url = https://raw.githubusercontent.com/tkgeeked/clash-rules-for-shadowrocket/main/loyalsoldier-whitelist.conf

[Rule]
# 应用直连
PROCESS-NAME,WeChat,DIRECT
PROCESS-NAME,QQ,DIRECT

# 局域网 IP
IP-CIDR,10.0.0.0/8,DIRECT
IP-CIDR,172.16.0.0/12,DIRECT
IP-CIDR,192.168.0.0/16,DIRECT

# 广告拦截
DOMAIN-SUFFIX,adserver.com,REJECT-DROP

# Apple / iCloud / Google 直连
DOMAIN-SUFFIX,apple.com,DIRECT
DOMAIN-SUFFIX,icloud.com,DIRECT

# GFW 列表
DOMAIN-SUFFIX,google.com,PROXY

# Telegram IP
IP-CIDR,91.108.56.0/22,PROXY

# 中国 IP
IP-CIDR,1.0.0.0/8,DIRECT

GEOIP,CN,DIRECT
FINAL,PROXY  # 白名单模式：默认走代理
```

### 黑名单模式

唯一区别在最后一行：
```
FINAL,DIRECT  # 黑名单模式：默认直连
```

## ⚠️ 注意事项

- 本规则**专为 Shadowrocket 设计**，不适用于 Clash 等其他客户端
- 规则数量较多（32 万+），可能对设备性能有一定影响
- 如果同时导入两个规则集会产生冲突，请只选择一个
- 部分网站可能需要手动调整规则以确保正常访问
- 如果导入后无法访问某些网站，请检查规则是否加载成功
- Apple、iCloud、Google 规则设置为直连，如需改为代理请手动编辑

## 🙏 鸣谢

本项目的规则数据完全来源于以下优秀项目：

- **Loyalsoldier/clash-rules**：[https://github.com/Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules)
  - 提供完整的 Clash Premium RULE-SET 规则集
  - 包含广告拦截、GFW、代理/直连域名、IP 地址等分类
  
- **Loyalsoldier/v2ray-rules-dat**：[https://github.com/Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)
  - 提供 v2ray 格式的规则数据
  
- **v2fly/domain-list-community**：[https://github.com/v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
  - 提供域名列表数据

- **gfwlist/gfwlist**：[https://github.com/gfwlist/gfwlist](https://github.com/gfwlist/gfwlist)
  - 提供 GFW 列表数据

- **felixonmars/dnsmasq-china-list**：[https://github.com/felixonmars/dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)
  - 提供 Apple 和 Google 在中国大陆可直连的域名列表

- **17mon/china_ip_list**：[https://github.com/17mon/china_ip_list](https://github.com/17mon/china_ip_list)
  - 提供中国大陆 IP 地址列表

感谢这些开源项目作者为社区做出的贡献！

## 📄 许可证

本项目遵循 [GPL-3.0 License](https://github.com/Loyalsoldier/clash-rules/blob/master/LICENSE) 许可证。

## 🤝 贡献

如果你发现问题或有改进建议，欢迎提交 Issue 或 Pull Request。
