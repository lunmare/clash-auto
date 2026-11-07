# Clash Auto

使用 `Clash-Auto.ini` 作为总模板文件名，沿用原有 INI 结构。以 ACL4SSR 的基础分流思路为骨架，直接引用多个维护活跃、拥有数千至数万 Star 的项目；不再人工整理、复制或提交域名清单。

## 模板地址

```text
https://raw.githubusercontent.com/lunmare/clash-auto/refs/heads/main/Clash-Auto.ini
```

在 SublinkPro 的规则配置导入处使用此地址。转换器需要支持 `clash-domain:`、`clash-ipcidr:`、`clash-classic:`。保持 INI 总模板和地区节点组，AI、流媒体等可分别选择出口。

## 上游及分工

| 上游 | 使用范围 |
|---|---|
| [ACL4SSR/ACL4SSR](https://github.com/ACL4SSR/ACL4SSR) | 局域网、放行、可选广告拦截、Apple、微软、Telegram、游戏、国外补充 |
| [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) | 海外 AI 总分类 |
| [SukkaW/Surge](https://github.com/SukkaW/Surge) | AI 补充、流媒体、下载、测速；引用其[官方成品镜像](https://github.com/SukkaLab/ruleset.skk.moe) |
| [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script) | GitHub、TikTok、Discord/Twitter/Facebook/Reddit/WhatsApp、国内媒体、YouTube/Spotify、Xbox |
| [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules) | 私有域名、基础代理、国内域名及中国/局域网 IP |

分类设计参考 [ACL4SSR_Online_Full.ini](https://github.com/ACL4SSR/ACL4SSR/blob/master/Clash/config/ACL4SSR_Online_Full.ini)，节点地区名称过滤沿用原 Clash-LIAN 模板。规则内容及其许可归各上游项目。

## 更新方式

所有规则直接指向上游，不依赖本仓库的定时任务。生成 `rule-providers` 时更新间隔为 86400 秒；若选择“展开规则”，需要更新订阅才会重新展开清单。Star 数量和活跃度是选源依据，不代表每份分类文件每天都有变更。

## 默认策略

| 分类 | 默认选择 |
|---|---|
| AI | 新加坡-自动，可另选日本、美国等出口 |
| GitHub、TikTok、Telegram、社交、流媒体、测速、国外 | 所有-自动 |
| Apple、微软、下载、游戏 | DIRECT，可按需改选代理 |
| 广告 | DIRECT；需要启用拦截时改选 REJECT |
| 国内与局域网 | DIRECT |
| 未命中 | 漏网之鱼，默认所有-自动 |

规则按顺序首次匹配：局域网与必要放行、AI、可选广告、服务分类、国外补充、国内域名和 IP、最终兜底。服务规则优先于基础国内外分类。默认保留使用者选择广告拦截的权利，避免直接套用上游全量广告屏蔽策略。

此仓库没有代理节点或凭据，节点仍由你自己的订阅提供。它与原仓库 `lunmare/clash` 独立，不读取旧库中的人工补充域名，因此不保证与旧清单逐条相同。

## ROS + OpenWrt 旁路由

模板只处理已经进入 Clash 的流量，不会自动修改 ROS 的 DNS 转发或策略路由。需要先让相关流量进入 OpenWrt；仅更新此模板不会补齐 ROS 尚未转发的域名。
