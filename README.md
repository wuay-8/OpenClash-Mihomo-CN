# OpenClash-Mihomo-CN

一份面向 **OpenClash + Mihomo** 的中国大陆网络环境配置模板。

项目目标是兼顾：

- 中国大陆环境下的冷启动能力
- OpenClash 友好的中文策略组
- Mihomo 现代配置结构
- Fake-IP + Sniffer
- MRS 规则集
- 国内 / 国际流量分流
- 常用 AI、流媒体、Google、Apple、Microsoft、Telegram 等服务分流
- 尽量减少对 GEOIP / country.mmdb 的依赖

---

## 📦 配置文件

主配置文件：

```text
Clash.yaml
```

GitHub Raw 地址：

```text
https://raw.githubusercontent.com/wuay-8/OpenClash-Mihomo-CN/main/Clash.yaml
```

OpenClash 中建议直接使用上面的 Raw 地址作为远程配置地址。

---

## ✨ 配置特点

### 1. 中国大陆冷启动

机场订阅通过 `DIRECT` 获取：

```yaml
proxy-providers:
  Airport:
    type: http
    url: "https://example.com/YOUR_SUBSCRIPTION_URL"
    proxy: DIRECT
```

启动逻辑：

```text
国内网络
   ↓
DIRECT 获取机场订阅
   ↓
加载代理节点
   ↓
建立代理能力
   ↓
通过代理更新 Rule Provider
   ↓
正常运行
```

这样可以减少首次启动时直接访问 GitHub Raw 失败的问题。

---

### 2. Rule Provider 通过代理更新

配置中使用独立策略组：

```text
🔧 规则下载
```

Rule Provider 在节点可用后通过该策略组进行更新。

---

### 3. 国内分流不依赖 GEOIP,CN

国内域名：

```text
CN.mrs
```

国内 IP：

```text
CN_IP.mrs
```

主规则中不再使用：

```yaml
GEOIP,CN
```

并关闭：

```yaml
geo-auto-update: false
```

目的是降低首次启动时对 `country.mmdb` / Geo 数据下载的依赖。

---

### 4. Fake-IP

使用：

```yaml
fake-ip-range: 198.18.0.1/16
```

同时保留常见局域网、NTP、STUN、微软联网检测、游戏设备等 Fake-IP 排除项。

---

### 5. Sniffer

启用：

- HTTP
- TLS
- QUIC

用于提升透明代理和 Fake-IP 环境下的域名识别能力。

---

## 🌍 节点策略组

配置包含：

```text
🚀 节点选择
🚀 手动切换
♻️ 自动选择
🔧 规则下载

🇭🇰 Hong Kong
🇯🇵 Japan
🇺🇸 United States
🇸🇬 Singapore
🇹🇼 Taiwan
🇰🇷 Korea
🇬🇧 United Kingdom
🇩🇪 Germany
🇫🇷 France
🌍 Other Regions
```

其中香港、日本、美国、新加坡、台湾包含自动测速策略。

---

## 🧭 分流策略组

包含常用业务分流：

```text
🌐 国际流量
🎯 国内流量
🚫 广告拦截
🤖 AI服务
📹 YouTube
🌍 国外媒体
✈️ Telegram
🔍 谷歌服务
📧 Google FCM
Ⓜ️ Microsoft
🍎 Apple服务
💳 PayPal
🎮 Steam
🫧 WeChat
```

---

## 🧠 AI 服务

当前 AI 策略覆盖：

- OpenAI / ChatGPT
- Claude / Anthropic
- Gemini
- Perplexity

默认更适合优先选择美国、新加坡、日本等节点。

---

## 📺 流媒体

当前主要覆盖：

- YouTube
- Netflix
- Disney+
- Max
- Spotify
- Bahamut
- Bilibili

没有保留大量低频流媒体 Rule Provider，以减少配置体积和维护成本。

---

## 🧩 Rule Provider

当前包括：

```text
AdBlock
AI
YouTube
Netflix
Spotify
Telegram
Google
Google FCM
Microsoft
Apple
Bilibili
Bahamut
TikTok
Disney
Max
PayPal
Steam
CN
CN_IP
Proxy
```

配置以 Mihomo MRS 为主，同时保留少量 classical 规则。

---

## 🚀 OpenClash 使用方法

进入：

```text
OpenClash
→ 配置订阅
→ 添加
```

订阅地址填写：

```text
https://raw.githubusercontent.com/wuay-8/OpenClash-Mihomo-CN/main/Clash.yaml
```

然后：

```text
保存配置
→ 更新配置
→ 启用配置
→ 重启 OpenClash
```

以后只要 GitHub 中的 `Clash.yaml` 内容更新，OpenClash 重新更新订阅即可获取最新版。

---

## ⚠️ 使用前必须修改

配置中默认机场地址是占位地址：

```yaml
proxy-providers:
  Airport:
    url: "https://example.com/YOUR_SUBSCRIPTION_URL"
```

你需要将其改成自己的 Clash / Mihomo 机场订阅地址。

---

## 🔐 安全提醒

本仓库是 **Public**。

不要把自己的真实机场订阅链接、Token、UUID、密码、私钥等敏感信息直接提交到公开仓库。

机场订阅链接通常本身就相当于账号凭证。

如果需要公开分享配置，建议始终保留：

```yaml
url: "https://example.com/YOUR_SUBSCRIPTION_URL"
```

真实订阅地址建议在本地 OpenClash 中单独管理。

---

## 🌐 中国大陆网络说明

部分 Rule Provider 使用 GitHub Raw。

本配置设计为：

```text
先获取机场节点
        ↓
建立代理
        ↓
通过 🔧 规则下载
        ↓
更新 Rule Provider
```

因此比所有规则都直接使用 `DIRECT` 下载更适合中国大陆网络环境。

前提是：

> 机场订阅地址本身能够在当前网络下直接访问。

如果机场订阅地址本身也必须翻墙才能访问，那么仍然可能出现冷启动问题。

---

## 🔄 更新方式

以后升级 V3 / V4 时，建议始终保持主文件名：

```text
Clash.yaml
```

只更新内容，不修改文件名。

这样 OpenClash 中的订阅地址可以长期保持不变：

```text
https://raw.githubusercontent.com/wuay-8/OpenClash-Mihomo-CN/main/Clash.yaml
```

---

## 📁 仓库结构

```text
OpenClash-Mihomo-CN
├── Clash.yaml
└── README.md
```

后续可以增加：

```text
CHANGELOG.md
rules/
docs/
examples/
```

---

## 📝 当前版本

```text
V2
```

主要特性：

- OpenClash + Mihomo
- 中国大陆冷启动
- Provider 化节点管理
- MRS 规则
- CN + CN_IP
- Fake-IP
- Sniffer
- 中文策略组
- 多地区节点分组
- 常用业务分流

---

## 📌 说明

本项目用于个人网络配置研究与维护。

不同机场节点命名方式、OpenClash 版本、Mihomo 内核版本和网络环境可能存在差异，如遇到节点筛选、Rule Provider 下载、DNS 或 Fake-IP 问题，需要根据实际环境调整。
