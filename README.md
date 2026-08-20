# OpenClash-Mihomo-CN

一份面向中国大陆网络环境的 Clash / Mihomo 配置模板。

当前版本：**V3**

主要兼容：

- OpenClash
- Mihomo
- Stash
- 塔台配置转换

项目目标：

- 中国大陆冷启动
- 稳定可靠
- 跨客户端兼容
- 清晰的节点分组
- 常用服务分流
- Fake-IP DNS
- Rule Provider 管理
- 后续维护方便

---

## V3 特点

- 无自动测速策略组
- 无 Emoji 策略组名称
- 无 MRS Rule Provider
- 使用普通 YAML / classical / ipcidr 规则
- 中国大陆冷启动
- Fake-IP DNS
- Sniffer
- 精确地区节点筛选
- 自动排除流量 / 到期 / 套餐提示节点
- OpenClash / Mihomo / Stash / 塔台兼容

---

## 配置文件

当前 V3 配置文件：

`Clash-V3.yaml`

Raw 地址：

`https://raw.githubusercontent.com/wuay-8/OpenClash-Mihomo-CN/main/Clash-V3.yaml`

---

## 中国大陆冷启动

机场订阅默认通过 `DIRECT` 获取。

核心结构：

`proxy-providers -> Airport -> proxy: DIRECT`

启动流程：

中国大陆网络  
↓  
DIRECT 获取机场订阅  
↓  
加载代理节点  
↓  
建立代理能力  
↓  
下载规则  
↓  
正常分流

这样可以降低首次启动时因为海外网络不可达而导致配置无法正常加载的概率。

---

## 节点策略组

V3 使用纯文字策略组名称。

主要节点组：

- 节点选择
- 手动切换
- 规则下载
- 香港
- 日本
- 美国
- 新加坡
- 台湾
- 韩国
- 英国
- 德国
- 法国
- 其他地区

所有地区组均为手动选择。

V3 不提供自动测速组。

---

## 业务分流

当前包含：

- 国际流量
- 国内流量
- 广告拦截
- AI服务
- YouTube
- 国外媒体
- Telegram
- Google
- Google FCM
- Microsoft
- Apple
- PayPal
- Steam
- WeChat

---

## AI 服务

主要覆盖：

- OpenAI
- ChatGPT
- Claude
- Anthropic
- Gemini
- Perplexity

建议优先使用美国、新加坡、日本节点。

---

## 流媒体

主要覆盖：

- YouTube
- Netflix
- Disney+
- Max
- Spotify
- Bahamut
- Bilibili
- TikTok

---

## Rule Provider

V3 当前包含 20 个 Rule Provider：

- AdBlock
- AI
- YouTube
- Netflix
- Spotify
- Telegram
- Google
- GoogleFCM
- Microsoft
- Apple
- Bilibili
- Bahamut
- TikTok
- Disney
- Max
- PayPal
- Steam
- CN
- CN_IP
- Proxy

---

## 为什么 V3 不使用 MRS

早期版本使用过 Mihomo MRS Rule Provider。

实际测试发现，在：

塔台  
↓  
生成 Stash 配置

这个流程中，部分 MRS 规则无法正常展开。

因此 V3 改为：

- 普通 YAML
- classical
- ipcidr

这样可以提高 OpenClash、Mihomo、Stash 和塔台之间的兼容性。

---

## 国内分流

国内流量主要通过：

- CN
- CN_IP

进行分流。

V3 主规则不依赖 `GEOIP,CN`。

同时关闭：

`geo-auto-update: false`

这样可以减少对 `country.mmdb` 和 GeoIP 数据的依赖。

---

## DNS

V3 使用 Fake-IP。

核心设置：

`enhanced-mode: fake-ip`

`fake-ip-range: 198.18.0.1/16`

基础 DNS：

- 223.5.5.5
- 119.29.29.29

DoH：

- https://dns.alidns.com/dns-query
- https://doh.pub/dns-query

---

## Sniffer

V3 启用：

- HTTP
- TLS
- QUIC

用于提高透明代理和 Fake-IP 环境下的域名识别能力。

---

## 地区节点筛选

V3 会自动识别：

- 香港 / Hong Kong / HK
- 日本 / Japan / JP
- 美国 / United States / US / USA
- 新加坡 / Singapore / SG
- 台湾 / Taiwan / TW
- 韩国 / Korea / KR
- 英国 / United Kingdom / UK / GB
- 德国 / Germany / DE
- 法国 / France / FR

同时排除：

- Traffic
- Expire
- 流量
- 剩余
- 到期
- 套餐
- 重置

避免机场提示节点进入地区分组。

---

## OpenClash 使用

进入：

OpenClash  
→ 配置订阅  
→ 添加

填写：

`https://raw.githubusercontent.com/wuay-8/OpenClash-Mihomo-CN/main/Clash-V3.yaml`

然后：

保存配置  
→ 更新配置  
→ 启用配置  
→ 重启 OpenClash

---

## 塔台 / Stash 使用

推荐流程：

Clash-V3.yaml  
↓  
塔台  
↓  
添加机场订阅  
↓  
生成配置  
↓  
导入 Stash

V3 已针对这个流程做兼容优化。

---

## 使用前必须修改

默认机场地址：

`https://example.com/YOUR_SUBSCRIPTION_URL`

只是占位符。

实际使用时需要替换为自己的 Clash / Mihomo 机场订阅地址。

---

## 安全提醒

本仓库为 Public。

请不要提交：

- 真实机场订阅地址
- Token
- UUID
- 密码
- 私钥
- API Key
- Cookie

机场订阅地址通常本身就相当于账号凭证。

公开版本建议始终保留占位地址：

`https://example.com/YOUR_SUBSCRIPTION_URL`

真实订阅地址请在本地配置。

---

## 推荐仓库结构

- Clash.yaml
- Clash-V2.1.yaml
- Clash-V2.2.yaml
- Clash-V2.2.1.yaml
- Clash-V3.yaml
- README.md

---

## 稳定版入口

建议 V3 测试稳定后，将 `Clash-V3.yaml` 的内容同步到：

`Clash.yaml`

这样长期可以使用固定地址：

`https://raw.githubusercontent.com/wuay-8/OpenClash-Mihomo-CN/main/Clash.yaml`

以后升级 V4、V5 时，只需要更新 `Clash.yaml` 内容，不需要修改客户端订阅地址。

---

## 版本记录

### V3

- 移除 Emoji
- 移除自动测速策略组
- 移除 MRS
- 改用普通 YAML Rule Provider
- 优化 Stash / 塔台兼容
- 优化 Fake-IP DNS
- 优化中国大陆冷启动
- 优化地区节点筛选
- 修复地区缩写误匹配
- 排除流量和到期提示节点

### V2.2.1

修复地区节点误匹配和提示节点问题。

### V2.2

解决塔台生成 Stash 配置时 MRS 规则无法正常展开的问题。

### V2.1

移除自动测速分组。

### V2

Provider 架构初始版本。

---

## 说明

本项目主要用于个人网络配置研究、学习与维护。

不同机场节点名称、OpenClash 版本、Mihomo 内核版本、Stash 版本和网络环境可能存在差异。

如果出现：

- 节点分类错误
- Rule Provider 下载失败
- DNS 异常
- Fake-IP 兼容问题

需要根据实际环境进一步调整。
