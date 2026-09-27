# 数据来源映射（Warning Dashboard → Live Feed）

主控台里的「预警仪表盘」每一项指标都需要可落地的实时数据源。下面给出免费、低门槛（多数无需 API key，手动即可核对；自动化时仅 Coinglass 免费档 + Alternative.me 免费 key 即可）的来源清单。把这张表当成「每天开盘前 5 分钟逐个打勾」的取数清单。

| # | 仪表盘指标 | 数据源 | 链接 | 读什么 | 频率 |
|---|---|---|---|---|---|
| 1 | 资金费率 Funding Rate | Coinglass | https://www.coinglass.com/pro/i/FundingRate | 主流合约资金费率，> +0.05% 预警 | 实时/小时 |
| 2 | 未平仓量 / 市值 OI·mcap | Coinglass | https://www.coinglass.com/ | OI 与市值比，衡量多头拥挤度 | 日 |
| 3 | 恐惧贪婪指数 F&G | Alternative.me | https://alternative.me/crypto/fear-and-greed-index/ | 数值 >75 贪婪 / <25 恐惧（反转区） | 日 |
| 4 | 稳定币交易所净流入 | DefiLlama / Artemis | https://defillama.com/ | 稳定币净流向 CEX（抄底弹药） | 日/周 |
| 5 | 单巨鲸大额开仓 | Lookonchain | https://x.com/lookonchain | 追踪 >$500M 异动、预置空单 | 实时推送 |
| 6 | 政策关键词 | 新闻 / Truth Social | — | 关税 / 利率 / 监管 关键词 | 事件驱动 |
| 7 | 交易所 ADL / 宕机 | 各所状态页 | 你所用交易所的官方 status 页面 | ADL 触发 / outage 公告 | 实时 |
| 8 | 现货 ETF 流量 | Farside | https://farside.co.uk/btc/ | BTC / ETH ETF 日净流入（机构真金白银） | 日 |
| 9 | 链上鲸鱼 / 持仓 | Arkham | https://arkhamintelligence.com/ | 鲸鱼地址异动、交易所净流量 | 实时 |

## 自动化取数（可选）
- **Alternative.me F&G API**：`https://api.alternative.me/fng/?limit=1` 返回 JSON，免费 key 可选。
- **Coinglass 免费档**：提供 funding / OI / liquidation 快照，注册即得 API key。
- **Farside ETF**：页面直接读，无 API；可定时爬取表格。
- **Lookonchain / Arkham**：以社交媒体推送 + 网页为主，适合做「异动告警」而非拉取。

## 使用纪律
- 手动核对时：开盘前 5 分钟按上表 1→9 逐条打勾（主控台 §1 已内置勾选框）。
- 任一项越过阈值 → 立即降低杠杆 / 移出抵押品，不等确认。
- 不要只盯单一所屏幕报价：极端行情下交叉验证（见技术因子手册「预言机幻影价格」）。

## 口径说明
数据以「官方披露 / 主流聚合器」为准；不同源对爆仓总额、日期标签存在分歧（如 $19.3B 官方 vs $30–40B 含延迟上报），所有数字在交付物中标注 `已坐实 / 存疑`。
