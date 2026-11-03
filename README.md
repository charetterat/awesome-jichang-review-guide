# 机场测评避坑清单：评测方法论、真实风险信号与验证工具 (updated 2026-11-03)

> 56 家机场一手流程记录沉淀出的测评框架：先验什么、再测什么、哪些宣传直接跳过

网上的机场推荐清单很多，讲「怎么自己测」的几乎为零。这份清单反过来：不告诉你哪家好，而是给你一套自己验证的方法——注册流程哪里最容易断、测速图哪三个地方最容易作假、AFF 返利怎么核、邮件静默丢弃怎么判。每一条都来自对 56 家机场的真实注册与实测流程记录，不是二手观点。

> [!NOTE]
> Methodology compiled from our own registration and verification workflow logs (Oct-Nov 2026). Linked tools are public resources — no affiliation unless marked.

## Contents

- [🚪 第一步：注册环节的五个真实卡点](#第一步注册环节的五个真实卡点)
- [📉 第二步：测速图的三个可信度检查点](#第二步测速图的三个可信度检查点)
- [💰 第三步：AFF 返利与价格的核验方法](#第三步aff-返利与价格的核验方法)
- [🧰 配套工具与参考](#配套工具与参考)

## 🚪 第一步：注册环节的五个真实卡点

来自 56 家机场注册流程的一手记录。注册失败不一定是你操作错——先分辨卡在哪一类，再决定是换浏览器、换邮箱还是直接放弃。

| Project | What it is | Tags |
|---|---|---|
| [A 类：邮件静默丢弃](https://www.mail-tester.com) | 最坑的一类：注册接口返回 success，验证码邮件永远不到（多数进了 Junk 或被发件方直接丢弃）。判据只有一个——看收件箱那侧，不看注册页的提示；可用 mail-tester 先排除收件方问题。 | `注册`, `邮件`, `验证码` |
| [B 类：CF 人机验证拦截](https://developers.cloudflare.com/cloudflare-challenges/) | Cloudflare Turnstile 在部分站是指纹级静默拦截——页面上根本没有可点的勾选框。同一浏览器人工访问能过、自动化访问过不了时，换浏览器环境重试一次，仍不行就记录并放弃。 | `Cloudflare`, `人机验证` |
| [C 类：必须购买才能注册](https://github.com/charetterat/awesome-jev-essentials) | 少数站要求先购买套餐才开放账号体系。这类站对只想先看面板的用户不友好，测评时应把「能不能零门槛注册」单独列为一项。 | `门槛` |
| [D 类：拖动滑块验证](https://www.cloudflare.com/products/turnstile/) | 滑块验证对自动化不友好，但人工通常能过。Turnstile 这类无感人机验证的原理见 Cloudflare 官方页面；遇到时记录即可，不必硬磕。 | `滑块` |
| [E 类：拆分式邮箱写死](https://datatracker.ietf.org/doc/html/rfc5321) | 个别站后端把邮箱域写死为 @gmail.com，用其他邮箱注册会返回 500（SMTP 层面的地址校验，见 RFC 5321）。表象是服务器错误，实际是站方限制——换 Gmail 邮箱即可注册成功。 | `邮箱`, `兼容性` |

## 📉 第二步：测速图的三个可信度检查点

测速图是机场宣传的核心物料，也是最容易掺假的地方。任何一张测速图，先过这三关再决定信多少。

| Project | What it is | Tags |
|---|---|---|
| [Speedtest by Ookla](https://en.wikipedia.org/wiki/Network_throughput) | 测速工具本身是中立的，问题在选择。看测速图先问三件事：几点测的（晚高峰还是凌晨）、哪个节点（本地还是机房附近）、跑了几次（挑最好的一次还是平均值）。 | `测速`, `工具` |
| [去程 ≠ 回程](https://en.wikipedia.org/wiki/Asymmetric_digital_subscriber_line) | 下载速度只证明回程。对上传有需求（直播、网盘同步、视频会议）的用户，回程快不等于可用——测评必须双向都测。 | `路由`, `双向` |
| [单次快照 ≠ 稳定性](https://en.wikipedia.org/wiki/Packet_loss) | 一张测速图是一个时间点的快照。真正的稳定性要看丢包率和跨天波动，一张漂亮的速度图证明不了这两件事。 | `稳定性`, `丢包` |

## 💰 第三步：AFF 返利与价格的核验方法

几乎所有机场清单都带推广链接，这不丢人——丢人的是不告诉你返利规则和核价日期。

| Project | What it is | Tags |
|---|---|---|
| [返利规则的三个数字](https://en.wikipedia.org/wiki/Affiliate_marketing) | 看推广规则只看三个数字：返利比例（如 5%）、封顶金额、到账条件。三者缺任何一项，这条推广规则就还不完整。 | `AFF`, `返利` |
| [价格快照日期](https://en.wikipedia.org/wiki/Value-added_tax) | 任何清单里的价格都必须带「核验日期」。机场价格变动频繁，没有日期的价格等于没有价格。 | `价格`, `核验` |
| [Credits ≠ 现金](https://en.wikipedia.org/wiki/Microtransaction) | 站内赠送的额度（Credits/余额）通常是消费抵扣用的站内资产，不是可以提现的现金。看到「送 XX 元」先分清是哪一种。 | `余额`, `提现` |

## 🧰 配套工具与参考

自己动手验证时用得到的公开工具，每样只做一件事。

| Project | What it is | Tags |
|---|---|---|
| [Speedtest by Ookla](https://www.speedtest.net/insights/blog/) | 最通用的带宽测速工具。测速时记录服务器位置与时间，才是可复现的证据；只截一张图不标时间等于没测。 | `工具`, `测速` |
| [BrowserLeaks DNS Leak Test](https://browserleaks.com/dns) | 检查 DNS 请求从哪里出去。VPN/代理场景下，DNS 走本地比走隧道更常见——这是「连上了但其实没保护」的头号原因。 | `工具`, `DNS`, `泄漏` |
| [ipinfo.io](https://ipinfo.io/) | 看出口 IP 的归属地与运营商（ASN）。机场宣传「日本节点」时，ASN 一查便知是机房还是家宽。 | `工具`, `IP`, `ASN` |
| [Check-Host](https://check-host.net/) | 从全球多个地点探测可达性与延迟，验证「某个地区能不能访问」不用自己满世界找朋友帮忙测。 | `工具`, `可达性` |
| [CAPTCHA 与人机验证](https://en.wikipedia.org/wiki/CAPTCHA) | 从 CAPTCHA 到无感 Turnstile 的演进背景。判断卡点前先读原理，再决定是换环境还是放弃。 | `工具`, `排障` |
| [姊妹篇：机场清单](https://github.com/charetterat/awesome-jev-essentials#readme) | 方法论之外，我们也维护按场景分流的机场信息整合仓库，两者配合使用。 | `清单` |

---

## About this list

- **17** entries across **4** sections.
- Compiled from public sources; every linked project carries its own license.
- Last updated: **2026-11-03**.
- Data lives in `data/content.json` — this README is generated, do not edit by hand.

## License

The text and curation in this repository are licensed under CC BY 4.0. Linked projects keep their own licenses.
