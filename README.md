# dedicated core vps: How to Get Guaranteed CPU Without Paying Dedicated-Server Prices

A dedicated core VPS gives you CPU cores that are physically pinned to your account, so a noisy neighbor on the same host can't steal your cycles. If your database queries spike at random hours, your game server stutters during peak times, or your monitoring shows a constant CPU steal percentage, this is the product category that fixes it. The catch: prices vary wildly, from about $10/month to $40+/month for similar core counts, and the fine print differs more than the spec sheets suggest.

This guide walks through what you actually get for your money, with GreenCloud's current EPYC VDS lineup as the main reference point, plus how it stacks up against other dedicated-core providers.

> **Quick picks**
> - Best overall value for dedicated cores: **GreenCloud EPYCVDS-1**, 1 dedicated EPYC Milan core, 8 GB RAM, 80 GB NVMe, 10 Gbps port, **$10/month** (USA/EU). Most people testing whether dedicated cores solve their CPU-steal problem should start here.
> - Running something compute-heavy in production: EPYCVDS-4 or -5, where the per-core cost drops as you scale.
> - On a tight budget and can tolerate shared or fair-share CPU: GreenCloud's Budget KVM line and its recent birthday-sale plans cost far less, but you give up the guaranteed cores.
>
> 👉 [Check current EPYC VDS pricing at GreenCloud](https://greencloudvps.com/billing/aff.php?aff=6679)

## What "dedicated core" actually means on a VPS

A dedicated core VPS sits between a regular cloud VPS and a bare-metal dedicated server. The physical machine is still shared with other tenants, but your CPU cores (and on plans like GreenCloud's, your RAM and NVMe storage too) are reserved exclusively for your instance. No other guest ever schedules work on them.

That distinction matters because the standard VPS problem isn't raw capacity, it's variance. On a shared-core plan, your neighbor's backup job or a badly behaved container eats into the same physical cores, and your p99 latency suffers even though your average CPU usage looks fine. One long-time LowEndTalk user described running a Mastodon instance, Nextcloud, Redis, and several Rails apps on GreenCloud's budget line, noting that the CPU steal stayed at zero; on plans where cores are genuinely pinned, that number stays at zero by design rather than by luck.

You give up two things compared to a dedicated server: the whole chassis is not yours (no IPMI, and neighbors still share your network uplink), and you can't get the same raw hardware. What you get back is speed of provisioning and resizing. A dedicated server typically takes hours to deploy; a VDS like GreenCloud's usually provisions in under 15 minutes, occasionally up to 2 hours.

## GreenCloud's dedicated core plans: the full lineup

GreenCloud runs its dedicated-core offering under the name **EPYC NVMe KVM VDS**. Every plan gets 100% dedicated physical AMD EPYC Milan cores, dedicated RAM, RAID-10 NVMe 4.0 storage, a 10 Gbps port, and Linux on KVM, with 24/7/365 support.

**USA/EU plans:**

| Plan | Dedicated cores | RAM | NVMe storage | Bandwidth | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| EPYCVDS-1 | 1× EPYC Milan | 8 GB | 80 GB | 4 TB | $10/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-2 | 2× EPYC Milan | 16 GB | 160 GB | 8 TB | $20/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-3 | 3× EPYC Milan | 24 GB | 240 GB | 12 TB | $30/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-4 | 4× EPYC Milan | 32 GB | 320 GB | 16 TB | $40/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-5 | 8× EPYC Milan | 64 GB | 640 GB | 16 TB | $80/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |

**APAC plans** (Singapore, Tokyo, Vietnam, Hong Kong) carry identical prices and hardware but roughly half the traffic at each tier:

| Plan | Dedicated cores | RAM | NVMe storage | Bandwidth (APAC) | Price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| EPYCVDS-1 | 1× EPYC Milan | 8 GB | 80 GB | 2 TB | $10/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-2 | 2× EPYC Milan | 16 GB | 160 GB | 4 TB | $20/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-3 | 3× EPYC Milan | 24 GB | 240 GB | 6 TB | $30/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-4 | 4× EPYC Milan | 32 GB | 320 GB | 8 TB | $40/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| EPYCVDS-5 | 8× EPYC Milan | 64 GB | 640 GB | 8 TB | $80/mo | [Order](https://greencloudvps.com/billing/aff.php?aff=6679) |

Two patterns worth noticing in those numbers. First, in both regions the top two tiers share the same bandwidth cap (16 TB in USA/EU, 8 TB in APAC), so stepping from EPYCVDS-4 to -5 buys you double the cores, RAM, and storage with no traffic penalty. Second, the per-core math holds up as you scale: EPYCVDS-5 works out to $10 per dedicated core — the same rate as the entry plan — but each core comes with 8 GB of RAM and 80 GB of NVMe attached, versus 8 GB and 80 GB for the whole EPYCVDS-1 box.

The pricing page shows monthly billing on the VDS line only; no annual discount is listed there. Sale events are a different story, covered below.

## What you'll actually pay over a year

Since the VDS line bills monthly, the sticker price is the real price: EPYCVDS-1 runs $120 over twelve months, EPYCVDS-4 runs $480. There's no intro-price-then-renewal-hike pattern to worry about here, which is refreshing in this market.

The number worth comparing isn't the monthly rate, though — it's what equivalent guaranteed CPU costs elsewhere:

| Provider / product | Dedicated cores | RAM | Storage | Price | Notes |
| --- | --- | --- | --- | --- | --- |
| GreenCloud EPYCVDS-1 | 1× EPYC Milan | 8 GB | 80 GB NVMe 4.0 | $10/mo | 4 TB traffic (USA/EU), 10 Gbps |
| GreenCloud EPYCVDS-4 | 4× EPYC Milan | 32 GB | 320 GB NVMe 4.0 | $40/mo | 16 TB traffic, 10 Gbps |
| Contabo Cloud VDS S | 6 dedicated vCores | 24 GB | — | from €37.13/mo | 24-month term pricing |
| RackWorks (Detroit) | 1 pinned physical core | 2 GB DDR4 ECC | 40 GB NVMe | from $18/mo | 1 Gbps, unlimited transfer, AVX-512 |
| Paragon | 4× AMD Zen 5 | 16 GB DDR5 | 200 GB NVMe | €29/mo | 10 Gbit/s port |
| HavenVPS | dedicated vCPU | — | — | from $39/mo | offshore locations |

These figures move, so treat them as a snapshot and verify against each provider's current page before deciding. What the table shows is that GreenCloud's entry tier undercuts most of the dedicated-core market on price per guaranteed core, while the bigger competitors win on RAM-per-dollar at the high end. Contabo's VDS S gives you six cores and 24 GB on a 24-month commitment for roughly €37/month; GreenCloud's closest match, EPYCVDS-5, is $80/month month-to-month but doubles the cores and RAM and lets you cancel anytime.

## When you don't need dedicated cores at all

Plenty of searches for dedicated core VPS come from people whose workload would run fine on a good shared-CPU plan. Web hosting, small APIs, VPN endpoints, hobby projects — none of these typically care about CPU steal.

GreenCloud's Budget KVM line is the usual landing spot. Sale plans have included configurations like 4 GB RAM / 2 cores / 35 GB NVMe / 4 TB traffic on 10 Gbps ports, with NVMe + EPYC Rome or Milan hardware at some locations and older E5v4 CPUs with SSD storage at others. Three things to know before buying one:

- **Sale plans are explicitly non-refundable.** Every Budget KVM sale listing carries a "No refund/Money back on this plan" notice. GreenCloud's own advice to buyers: test the datacenter IP before committing.
- **Hardware varies by node.** The same plan tier can mean a modern EPYC/NVMe machine in one city and an E5v4/SSD machine in another. Check the location details, since the older CPUs show their age under load.
- **Stock moves fast on popular nodes.** During recent sale windows, NVMe/EPYC locations repeatedly sold out while E5v4/SSD nodes kept inventory, so if a specific location matters to you, timing is part of the purchase.

The panel is VirtFusion, Linux only, and each plan includes one free backup/snapshot slot. There's also a regular Ryzen KVM line starting at $6/month for 1 core at 3.5+ GHz, 1 GB RAM, and 15 GB NVMe, if you just need something cheap and Linux-native.

👉 [Compare GreenCloud's full plan lineup and current stock](https://greencloudvps.com/billing/aff.php?aff=6679)

## The fine print that actually affects your decision

Three policy details don't show up in any comparison table but should shape when and how you buy.

**Refunds are narrow.** GreenCloud's general refund window is 7 days, applies to your first service only, and excludes sale plans and payments made with cryptocurrency. Sale-tier plans — the cheap annual deals — are non-refundable from the moment you pay, and that explicitly includes the recent birthday-sale plans. If you're the type who buys, benchmarks for a week, and decides, the monthly VDS plans within that 7-day first-service window are the safe path; the annual sale machines are not.

**It's unmanaged.** GreenCloud handles the hardware, network, and uptime (they guarantee 99.99% for network and power, with a public status record), but OS configuration, software problems, and application issues are yours. Standard for budget VPS, but worth stating.

**Promo events have their own rules.** GreenCloud ran a 13th birthday sale from October 26–31, 2026 (UTC+0), and stated up front that there would be no Black Friday promotion this year — that sale was the season's only major event. Its headliner was the "1313" plan: 13 GB RAM, 113 GB NVMe 4.0, 6 fair-share EPYC Milan cores, a 10 Gbps port, and 12 TB of traffic at USA/EU locations (3333 GB at the Tokyo Softbank/IIJ nodes), priced at **$123 for three years** — roughly $3.42/month. Note the wording: fair-share cores, not dedicated ones, so it's a budget option rather than a rival to the VDS line. The event also ran flash sales every 1–2 hours on its LowEndTalk thread, a 13% account-credit cashback on purchases over $500, and a renewal guarantee: older promotional plans keep renewing at their original price, no increases. Past events have included perks like doubled RAM and traffic on three-year prepayments for some plans.

The renewal guarantee is more valuable than it sounds. Long-term followers of GreenCloud's sales know the annual deals can be dramatic — one blogger who tested a Japan Softbank EPYC plan at $35/year said he'd buy it again without hesitation if it reappeared in an event, and another user picked up a 4-core/8 GB Japan Softbank box at $45/year. Prices like that are why the non-refundable rule bites: you're buying a cheap machine sight unseen.

👉 [Check GreenCloud's current prices, plans, and refund terms before ordering](https://greencloudvps.com/billing/aff.php?aff=6679)

## What real users report

The public record is mixed, and it's worth reading both sides before spending money.

On the positive side, LowEndTalk users have voted GreenCloud the community's #1 provider in 2024 and 2025, and long-term users of 3–5+ years consistently mention stability and price. The zero-CPU-steal experience on the budget line, cited earlier, came from someone running multiple production apps on it. GreenCloud's own pages claim an average ticket response of 9 minutes; a third-party review measured it closer to 12. Either figure is fast for this price bracket.

On the negative side, Trustpilot's recent reviews (October 2026 in particular) document several frustrating cases: a customer who renewed a Japan VPS for its advertised China-optimized network, found it unreachable from mainland China after renewal, and was repeatedly pointed to the non-refundable policy (GreenCloud's support acknowledged the IP range was likely blocked by the GFW and offered a $2 IP change or a wait for a new range); a buyer whose PayPal option never appeared at checkout during the anniversary sale, whose ticket was closed without resolution; and reports of servers being suspended or cancelled with little explanation. One customer was charged a $5 recreation fee to restore a VPS they'd cancelled by mistake.

Even fans of the Japan Softbank line report "great by day, mediocre by night" — evening-peak packet loss shows up in multiple accounts, though the $45/year customer running a WeChat AI bot on his box called the impact minor for that use case.

The pattern in the complaints isn't hardware quality — it's after-sales policy enforcement. Non-refundable sale plans plus strict policy application means the company rarely makes exceptions, so the practical advice is simple: use the monthly VDS plans and the 7-day window to validate that a location and route work for you before committing to any longer or cheaper arrangement.

## Questions people ask before buying

**Is a dedicated core VPS worth it over a regular VPS?** If you run databases, game servers, CI runners, or anything latency-sensitive, yes — CPU steal is the difference between consistent and erratic performance under load. For static sites and light apps, it's paying for headroom you won't use.

**Does GreenCloud's VDS include Windows?** The EPYC VDS plans are listed as Linux. GreenCloud sells separate Windows VPS plans (Hyper-V based) if you need RDP out of the box.

**How fast is provisioning?** Usually under 15 minutes after payment, occasionally up to 2 hours. Sale events can be slower given the order volume.

**Can I upgrade later?** The Budget KVM line documents add-ons at $3 per extra GB of RAM, $3 per extra core, and $3 per 10 GB of SSD monthly, subject to node availability. The VDS line is structured as fixed tiers, so a bigger workload usually means moving up a plan.

**What about APAC locations?** Singapore, Tokyo, Vietnam, and Hong Kong are available on the VDS line at the same prices as USA/EU, with half the traffic. For China-facing routes, GreenCloud markets optimized lines (IIJ and Softbank in Tokyo), but as the Trustpilot case shows, no provider can guarantee a route stays usable from mainland China indefinitely.

**Do promo plans renew at the same price?** GreenCloud has committed to keeping older promotional plans at their original renewal price, even while stating that hardware and datacenter costs have risen. If you hold one of those legacy deals, keeping it active is generally the right call.

## Picking a plan, in one pass

Running a production database, game server, or anything where CPU variance costs you money → **EPYCVDS-2 or -3**, the sweet spot between headroom and price. Testing whether dedicated cores fix your problem → **EPYCVDS-1 at $10/month**, inside the 7-day first-service refund window. Need serious compute with no long commitment → **EPYCVDS-5**, where 8 cores and 64 GB at $80/month works out to the same $10-per-core rate as the entry plan, with far more attached hardware. Tight budget, shared CPU is fine → the Budget KVM and event-sale plans, with eyes open about the no-refund rule and the hardware lottery between EPYC/NVMe and E5v4/SSD nodes.

Two last checks before you order. First, confirm the location against what the server actually needs to reach: traffic halves in APAC, routes to mainland China aren't guaranteed to stay open, and monthly billing on the VDS line is your friend until you've verified route quality yourself. Second, mind the checkout mechanics — unpaid orders auto-cancel after 30 minutes, and new customers create their account during checkout rather than before, so have your registration details and payment method ready, especially if you're timing a restock or a flash sale.

👉 [Order the EPYC VDS plan that fits your workload](https://greencloudvps.com/billing/aff.php?aff=6679)
