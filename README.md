# Awesome Build for Korea [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

![resources](https://img.shields.io/badge/resources-80%2B-coral) ![last verified](https://img.shields.io/badge/verified-2026--06--10-blue) ![license](https://img.shields.io/badge/license-CC0-lightgrey)

> Everything you need to ship a product into the Korean market, curated for foreign and AI-assisted builders.

Korea runs on a different stack than the West. Stripe coverage is thin, Google Maps barely works, identity verification is often mandatory, and KakaoTalk (not email or SMS) is the channel users expect. The official docs are usually Korean-only, and most services assume you already hold a Korean account, phone number, and business registration.

This list is the map through that wall. Every entry is annotated for the things a non-Korean builder actually needs to know: **is there an MCP server or SDK, are the docs in English, and can you even sign up from outside Korea?**

What is curated here is the **builder's stack**: the resources you reach for at each layer of shipping into Korea, judged by how usable they are from abroad. The aim is breadth with honest annotations, not a raw dump of every Korean API.

### How to read the foreigner-access signal

The 🛂 column is the whole point of this list, and it is also the hardest thing to get right. **✅** means confirmed usable from abroad with no Korean presence. **⚠️** means there are hurdles *or* the access path could not be fully confirmed (treat it as "verify before you build"). **❌** means confirmed blocked without a Korean presence.

This axis is about a Korean *presence*, not nationality. A "presence" means either a Korean business entity or Korean residency via an Alien Registration Card (ARC / 외국인등록증). Foreign residents with an ARC can complete real-name verification (본인인증) and obtain a joint certificate (공동인증서), so do not read "needs 본인인증" as "Korean citizens only." Genuine citizenship-only gates are rare and flagged explicitly (KOSIS is the one confirmed case). Friction changes often: check the official source before you commit, and please open a PR or issue if you find a rating is wrong.

## Legend

| Signal | Meaning |
|---|---|
| 🌐 **Docs** | `EN` English available · `KO` Korean only · `EN~` partial English |
| 🔑 **Auth** | `key` API key · `oauth` OAuth · `cert` requires Korean joint certificate (공동인증서) · `none` no auth |
| 🛂 **Access** | ✅ usable from abroad, no Korean presence · ⚠️ hurdles or unconfirmed · ❌ Korean entity or residency (ARC) required |
| 💰 **Cost** | `free` · `freemium` · `paid` |
| 🤖 **AI** | `MCP` Model Context Protocol server exists · `SDK` official SDK · `REST` REST only |

## Contents

- [🤖 AI Builders Start Here](#-ai-builders-start-here)
- [🪪 Identity & Authentication](#-identity--authentication)
- [💳 Payments](#-payments)
- [🗺️ Maps & Location](#️-maps--location)
- [🏠 Address & Postcode](#-address--postcode)
- [💬 Messaging & Channels](#-messaging--channels)
- [🧠 AI / LLM for Korean](#-ai--llm-for-korean)
- [🔌 MCP Servers](#-mcp-servers)
- [🏛️ Public & Government Data](#️-public--government-data)
- [🛒 Commerce & Logistics](#-commerce--logistics)
- [⚖️ Compliance Gotchas](#️-compliance-gotchas)
- [Contributing](#contributing)

---

## 🤖 AI Builders Start Here

If you are building with Claude, Cursor, or another agent and want it to call Korean services directly, start with the resources that already ship an MCP server or a clean SDK. The zero-friction starter pack below is everything an agent can reach from abroad with a free key.

| Resource | What your agent gets | 🌐 | 🛂 | 🤖 |
|---|---|---|---|---|
| [PortOne MCP](https://github.com/portone-io/mcp-server) | Payments across Toss, KakaoPay, NaverPay, Korean card PGs through one endpoint (official) | EN | ✅ | MCP |
| [korea-stock-mcp](https://github.com/jjlabsio/korea-stock-mcp) | DART disclosures + KRX (KOSPI/KOSDAQ) prices and filings | KO | ✅ | MCP |
| [law-mcp](https://github.com/finalchild/law-mcp) | Korean statutes via the national law database (law.go.kr) | KO | ✅ | MCP |
| [KMA-WEATHER-MCP](https://github.com/woongaro/KMA-WEATHER-MCP) | Korea Meteorological Administration forecasts and conditions | KO | ✅ | MCP |
| [Upstage Solar](https://www.upstage.ai) | Bilingual Korean/English LLM, OpenAI-compatible, global signup | EN | ✅ | SDK |

See the full [MCP Servers](#-mcp-servers) section for more.

<sub>[↑ back to top](#contents)</sub>

---

## 🪪 Identity & Authentication

The biggest surprise for foreign builders: many Korean services require **real-name identity verification (본인인증)**, which routes through six government-designated providers. The integration barrier is a Korean business to contract with the provider, not nationality: a foreign resident with an Alien Registration Card (ARC / 외국인등록증) can themselves complete 본인인증 as an end user. For consumer login, Kakao and Naver OAuth are the pragmatic path.

**Real-name verification (본인인증)**

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [NICE CheckPlus (NICE평가정보)](https://www.niceapi.co.kr/) | Phone/card/i-PIN identity verification; returns CI/DI for user dedup | KO | key | ⚠️ Korean business contract required | paid | REST |
| [KCB OKname (코리아크레딧뷰로)](https://www.ok-name.co.kr/) | Phone/card/i-PIN verification; largest ID-data custodian | KO | key | ⚠️ Korean business contract required | paid | REST |
| [SCI평가정보 / Siren24](https://www.sci.co.kr/) | Government-designated verification; phone, i-PIN (마이핀) | KO | key | ⚠️ Korean business contract required | paid | REST |
| [BaroCert (바로써트)](https://www.barocert.com/) | Aggregator for Kakao/Naver/Toss 간편인증; SDKs in 5+ languages | KO | key | ⚠️ unverified onboarding | paid | SDK |

**Social / OAuth login**

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Kakao Login (카카오 로그인)](https://developers.kakao.com/docs/latest/en/kakaologin/rest-api) | OAuth + OIDC; ~47M users; English docs | EN | oauth | ✅ foreign phone accepted; business verification at scale | free | SDK |
| [Naver Login (네이버 로그인)](https://developers.naver.com/docs/login/overview/overview.md) | OAuth; dominant portal login | EN~ | oauth | ⚠️ Korean-only portal, app review | free | REST |
| [Apple Sign In](https://developer.apple.com/sign-in-with-apple/) | Standard Apple OAuth; mandatory if your iOS app offers third-party login | EN | oauth | ✅ global Apple Developer Program | paid | SDK |
| [Google Sign-In](https://developers.google.com/identity) | Standard Google OAuth; common among younger Korean users | EN | oauth | ✅ global GCP | free | SDK |

**Simple authentication (간편인증, app-based, no resident number)**

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Kakao Certification / Business Auth](https://developers.kakao.com/docs/latest/en/business-auth/rest-api) | KakaoTalk-based identity auth; CI/DI via designated channel | EN | oauth | ⚠️ business verification required | freemium | REST |
| [Toss Certification (토스인증서)](https://toss.im/tosscert/docs/guides/integration/user) | Toss-app identity auth; integrable directly or via BaroCert | KO | oauth | ⚠️ unverified, contact required | paid | REST |
| [Naver Certificate (네이버 인증서)](https://developers.naver.com/) | Naver-app identity auth; usually via BaroCert | KO | oauth | ⚠️ Korean-only portal | freemium | REST |

<sub>[↑ back to top](#contents)</sub>

---

## 💳 Payments

Stripe coverage in Korea is partial, so builders use a Korean payment gateway (PG) plus the wallet trio (KakaoPay, Naver Pay, Toss). The practical split: **aggregators and global merchant-of-record platforms let you accept Korean methods without a Korean entity; direct PG contracts almost always require one.**

**Aggregators (one API, many Korean PGs)**

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [PortOne (포트원)](https://portone.io/) | Single API fronting all major Korean PGs + wallets; official MCP server | EN~ | key | ⚠️ Korean business to go live (sandbox open) | freemium | MCP |
| [PortOne Global](https://portone.io/) | Cross-border orchestration for non-Korean entities (SEA + Korea) | EN | key | ✅ built for global merchants | paid | SDK |
| [Bootpay (부트페이)](https://www.bootpay.co.kr/) | Lighter PG aggregator popular with Korean indie devs | KO | key | ⚠️ unverified | freemium | SDK |

**Direct payment gateways (PG)**

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Toss Payments (토스페이먼츠)](https://www.tosspayments.com/) | #2 PG by volume; strong DX; covers cards + all wallets | EN~ | key | ⚠️ Korean business to go live | paid | SDK |
| [NICEPAY (나이스페이먼츠)](https://www.nicepay.co.kr/) | Long-standing PG; Stripe's local processor; English GitHub manual | EN~ | key | ⚠️ Korean business registration | paid | SDK |
| [KG Inicis (KG이니시스)](https://www.inicis.com/) | #1 PG by transaction volume | KO | cert | ⚠️ Korean business; integrate via PortOne | paid | REST |
| [NHN KCP](https://kcp.co.kr/) | 3rd-largest PG; English developer portal | EN~ | cert | ⚠️ Korean e-commerce compliance audit | paid | REST |
| [Danal (다날)](https://developers.danalpay.com/) | Carrier billing (통신과금) leader; also cards/gift cards | KO | key | ⚠️ Korean business (사업자번호 required) | paid | REST |

**Consumer wallets** (accept via an aggregator or PG, not direct)

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [KakaoPay (카카오페이)](https://pay.kakao.com/) | ~30M+ users; in-app/web/QR; one-time + recurring | KO | oauth | ⚠️ via Stripe/Paddle/KOMOJU/PortOne | paid | REST |
| [Naver Pay (네이버페이)](https://pay.naver.com/) | ~30M MAU; strong in SmartStore ecosystem | KO | key | ⚠️ via aggregator/PG | paid | REST |
| [Toss Pay (토스페이)](https://pay.toss.im/) | Toss app wallet (distinct from Toss Payments) | KO | key | ⚠️ via KOMOJU/Paymentwall | paid | REST |
| [PAYCO](https://www.payco.com/) | NHN wallet; strong in gaming/entertainment | KO | key | ⚠️ via Stripe/Paddle/KOMOJU | paid | REST |
| [Samsung Pay](https://pay.samsung.com/developers) | NFC + MST device wallet; ~18% of KR mobile payments | EN | cert | ⚠️ Samsung partnership application | paid | SDK |
| [Apple Pay](https://developer.apple.com/apple-pay/) | Works globally, but Korea card coverage is very limited | EN | oauth | ✅ but low KR conversion impact | free | SDK |

**Global options that work for Korea without a Korean entity**

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Stripe (Korea methods)](https://docs.stripe.com/payments/countries/korea) | Local cards + KakaoPay/NaverPay/PAYCO/Samsung Pay via NICEPay; KRW, recurring | EN | key | ✅ available to accounts in 29 countries | paid | SDK |
| [Paddle](https://www.paddle.com/) | Merchant of record; KRW, local cards + wallets; tax handled | EN | key | ✅ no Korean entity or bank needed | paid | SDK |
| [KOMOJU](https://en.komoju.com/payment-methods/korea/) | Korean cards + KakaoPay/NaverPay/Toss/PAYCO + carrier billing | EN | key | ✅ no local entity for most methods | paid | SDK |
| [Paymentwall](https://www.paymentwall.com/) | KakaoPay/Toss/PAYCO for foreign merchants via one API | EN | key | ⚠️ verify (last confirmed 2020) | paid | SDK |

<sub>[↑ back to top](#contents)</sub>

---

## 🗺️ Maps & Location

Google Maps is intentionally limited in Korea (no driving directions, sparse data) because map-data export is legally restricted. Kakao and Naver have licensed the full-resolution government data, so use them instead.

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Kakao Maps + Local API](https://developers.kakao.com/docs/latest/en/local/dev-guide) | Map display, place/keyword search, geocoding, reverse geocoding, coord transforms | EN | key | ✅ foreign phone accepted (3-5 day review) | freemium | MCP |
| [Kakao Navi](https://developers.kakao.com/) | Turn-by-turn route data and navigation deeplinks | KO | key | ✅ same Kakao account | freemium | REST |
| [Naver Maps (Naver Cloud Platform)](https://guide.ncloud-docs.com/docs/en/maps-overview) | Map SDKs, Static Map, Directions (5/15 waypoints), geocoding; richest KR data | EN | key | ⚠️ personal needs KR phone + ARC; business accounts in 15 countries | freemium | MCP |
| [TMap API (SK Telecom)](https://tmapapi.tmapmobility.com/main.html) | Maps, car/truck/pedestrian routing, POI, traffic, geofencing | KO | key | ⚠️ unverified (SK Open API, KR-only portal) | freemium | REST |
| [TMap Transit API](https://transit.tmapmobility.com/) | Optimal public-transit routing (bus/subway/rail/ferry) | KO | key | ⚠️ unverified | freemium | REST |
| [VWorld (국토정보플랫폼)](https://www.vworld.kr) | Government 2D/3D tiles, aerial imagery, DEM, boundaries, geocoder | KO | key | ⚠️ unverified (KR gov portal) | free | REST |

> Community MCP servers exist for Kakao Maps ([place search](https://github.com/cgoinglove/mcp-server-kakao-map), [navigation](https://github.com/CaChiJ/kakao-navigation-mcp-server)) and [Naver Maps](https://github.com/num2k/naver-map-mcp). See [MCP Servers](#-mcp-servers).

<sub>[↑ back to top](#contents)</sub>

---

## 🏠 Address & Postcode

Korean addresses come in two systems (road-name 도로명주소 and land-lot 지번주소), and proper handling is its own problem.

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Juso Road-Name Address API (행정안전부)](https://www.juso.go.kr/openEngPage.do) | Authoritative address lookup + structured codes + embeddable popup | EN~ | key | ⚠️ Korean phone (본인인증) or i-PIN to register | free | REST |
| [Kakao Address Search (Local API)](https://developers.kakao.com/docs/latest/en/local/dev-guide) | Address-to-coords and reverse, road-name + land-lot, JSON/XML | EN | key | ✅ same Kakao account path | freemium | REST |
| [Daum Postcode Service](https://postcode.map.daum.net/guide) | The de facto embeddable postcode/address widget for web forms | KO | none | ✅ no signup, script embed only | free | REST |

> Daum Postcode is the only entry in this list with zero registration friction: no key, two lines of script.

<sub>[↑ back to top](#contents)</sub>

---

## 💬 Messaging & Channels

In Korea, KakaoTalk (not email or SMS) is the channel users expect for transactional and marketing messages. **Prerequisite for any AlimTalk/FriendTalk:** you must hold a verified KakaoTalk Channel (카카오톡 채널, registered at center-pf.kakao.com) and get each message template pre-approved by Kakao. The channel step is doable from abroad with foreign business documents, but the console is Korean-only.

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [NHN Cloud KakaoTalk Bizmessage](https://docs.nhncloud.com/en/Notification/KakaoTalk%20Bizmessage/en/alimtalk-api-guide/) | AlimTalk (알림톡) + FriendTalk (친구톡) + SMS, fully English-documented | EN | key | ✅ international signup (still needs channel + template approval) | freemium | REST |
| [Naver Cloud SENS](https://guide.ncloud-docs.com/docs/en/sens-overview) | SMS + international SMS + AlimTalk + FriendTalk + 080 opt-out | EN | key | ⚠️ some country restrictions, contact support | freemium | REST |
| [Kakao i Connect Message (dk techin)](https://docs.kakaoi.ai/kakao_i_connect_message/bizmessage_eng/) | Official Kakao-licensed AlimTalk/FriendTalk/SMS/RCS platform | EN | oauth | ⚠️ channel + service contract | paid | REST |
| [Solapi (솔라피)](https://solapi.com/) | Popular CPaaS reseller; AlimTalk, SMS/LMS/MMS, RCS; SDKs in 6 languages | KO | key | ⚠️ unverified (phone-verified signup) | freemium | SDK |
| [Aligo (알리고)](https://smartsms.aligo.in/alimapi.html) | Budget SMS + AlimTalk reseller popular with KR SMBs | KO | key | ⚠️ unverified | freemium | REST |
| [Bizm (비즈엠)](https://alimtalk-api.bizmsg.kr/) | AlimTalk + SMS reseller used by KR logistics/commerce | KO | key | ⚠️ unverified | paid | REST |
| [Infobip KakaoTalk](https://www.infobip.com/docs/kakaotalk) | Enterprise CPaaS, English AlimTalk/FriendTalk | EN | key | ⚠️ Korean business license required for channel | paid | REST |
| [Sinch KakaoTalk](https://developers.sinch.com/docs/conversation/channel-support/kakaotalk) | AlimTalk/FriendTalk via unified Conversation API | EN | key | ⚠️ channel + template approval | paid | REST |
| [Twilio (Korea SMS)](https://www.twilio.com/en-us/guidelines/kr/sms) | Standard SMS/MMS to KR numbers (no KakaoTalk) | EN | key | ✅ fully self-serve | paid | SDK |
| [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) | Push on all major Korean Android OEMs (Samsung dominant) | EN | key | ✅ no KR restriction | free | SDK |

<sub>[↑ back to top](#contents)</sub>

---

## 🧠 AI / LLM for Korean

Models and APIs that handle Korean well. **Upstage Solar is the foreigner-friendly default** (global signup, no Korean entity, OpenAI-compatible). Naver's CLOVA stack is the strongest on Korean nuance once you have a Naver Cloud Platform (NCP) account.

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Upstage Solar](https://www.upstage.ai) | Bilingual KR/EN LLM, OpenAI-compatible endpoint | EN | key | ✅ global signup, no KR entity | freemium | REST |
| [HyperCLOVA X (CLOVA Studio)](https://www.ncloud.com/product/aiService/clovaStudio) | Naver's native Korean hyperscale LLM | EN~ | key | ⚠️ NCP account (regions KR/JP/SG/DE/US) | freemium | SDK |
| [Kakao Kanana-2](https://github.com/kakao/kanana) | Kakao's bilingual open-weight LLM (30B MoE) | EN~ | key | ✅ HF weights global (CC-BY-NC, commercial needs license) | freemium | SDK |
| [LG EXAONE 4.5](https://github.com/LG-AI-EXAONE/EXAONE-4.5) | LG's open-weight multilingual LLM; serverless via FriendliAI | EN~ | key | ✅ weights on HF; FriendliAI global | freemium | SDK |
| [CLOVA Speech (STT)](https://api.ncloud-docs.com/docs/en/ai-naver-clovaspeechrecognition-stt) | Korean/EN/JA speech-to-text (NEST engine) | EN | key | ⚠️ NCP account | freemium | REST |
| [CLOVA Voice (TTS)](https://api.ncloud-docs.com/docs/en/ai-naver-clovavoice) | Korean neural text-to-speech | EN | key | ⚠️ NCP account | freemium | REST |
| [Return Zero / RTZR (STT)](https://developers.rtzr.ai/docs/en/) | Popular Korean + Japanese STT; 600 free minutes | EN | key | ✅ open signup | freemium | REST |
| [Papago Translation (Naver)](https://api.ncloud-docs.com/docs/en/ai-naver-papagonmt) | KO↔EN/ZH/JA NMT; text, image, doc, website | EN | key | ⚠️ NCP account | freemium | REST |
| [KoNLPy](https://konlpy.org/) | Python wrapper for 5 Korean morphological analyzers | EN~ | none | ✅ pip install | free | SDK |
| [Kiwi (kiwipiepy)](https://github.com/bab2min/Kiwi) | Fast Korean morphological analyzer + typo correction; many bindings | EN~ | none | ✅ pip install | free | SDK |
| [soynlp](https://github.com/lovit/soynlp) | Unsupervised Korean tokenizer/noun extractor (maintenance-mode) | KO | none | ✅ pip install | free | SDK |
| [KLUE / KLUE-BERT](https://github.com/KLUE-benchmark/KLUE) | 8-task Korean NLU benchmark + pretrained baselines | EN | none | ✅ via Hugging Face | free | SDK |

<sub>[↑ back to top](#contents)</sub>

---

## 🔌 MCP Servers

Real, repo-confirmed MCP servers for Korean services, so an agent (Claude, Cursor) can call them. Tagged **official** (vendor-maintained) or **community**. For the full catalog (50+), see [awesome-mcp-korea](https://github.com/darjeeling/awesome-mcp-korea).

| Server | What it exposes | Source | 🌐 | 🛂 | 💰 |
|---|---|---|---|---|---|
| [PortOne MCP](https://github.com/portone-io/mcp-server) | PortOne payment docs, channels, payment history | official | EN | ✅ | free |
| [PortOne Global MCP](https://github.com/iamport-intl/portone-global-mcp-server) | PortOne Global docs + OpenAPI schemas | official | EN | ✅ | free |
| [korea-stock-mcp](https://github.com/jjlabsio/korea-stock-mcp) | DART disclosures + KRX prices/financials | community | KO | ✅ | free |
| [law-mcp](https://github.com/finalchild/law-mcp) | Korean statutes via law.go.kr | community | KO | ✅ | free |
| [assembly-api-mcp](https://github.com/hollobit/assembly-api-mcp) | National Assembly bills, schedules, budget | community | KO | ✅ | free |
| [mcp-korea-tourism-api](https://github.com/harimkang/mcp-korea-tourism-api) | Korea Tourism Org attractions/events/stays | community | EN~ | ✅ | free |
| [KMA-WEATHER-MCP](https://github.com/woongaro/KMA-WEATHER-MCP) | Korea Meteorological Administration forecasts | community | KO | ✅ | free |
| [kakao-navigation-mcp-server](https://github.com/CaChiJ/kakao-navigation-mcp-server) | Kakao geocode + routing + transit + place search | community | KO | ⚠️ Kakao key | free |
| [mcp-server-kakao-map](https://github.com/cgoinglove/mcp-server-kakao-map) | Kakao place/restaurant recommendations | community | KO | ⚠️ Kakao key | free |
| [naver-map-mcp](https://github.com/num2k/naver-map-mcp) | Naver geocoding, reverse geocoding, Directions 5/15 | community | KO | ⚠️ NCP key | free |
| [data-go-mcp-servers](https://github.com/Koomook/data-go-mcp-servers) | data.go.kr business info, procurement, financials | community | KO | ⚠️ data.go.kr key | free |
| [ko-stdict-mcp](https://github.com/dahlia/ko-stdict-mcp) | Standard Korean Dictionary (국립국어원) | community | KO | ✅ | free |
| [mcp-korean-spell](https://github.com/winterjung/mcp-korean-spell) | Korean spell and grammar checker | community | KO | ✅ | free |

<sub>[↑ back to top](#contents)</sub>

---

## 🏛️ Public & Government Data

One [data.go.kr](https://www.data.go.kr/en/index.do) account (email signup, no Korean phone) unlocks a large slice of the government data ecosystem. Some agency portals are harder, and KOSIS is confirmed citizenship-gated.

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Public Data Portal (data.go.kr)](https://www.data.go.kr/en/index.do) | Gateway to 70,000+ government datasets; issues keys for many agency APIs | EN~ | key | ✅ English portal, email signup | free | MCP |
| [MOLIT Real-Estate Prices (실거래가)](https://www.data.go.kr/data/15126469/openapi.do) | Apartment/villa/officetel sale + jeonse/wolse transactions since 2006 | KO | key | ✅ inherits data.go.kr account | free | MCP |
| [KMA Weather API Hub (기상청)](https://apihub.kma.go.kr/) | Forecasts, observations, radar, satellite, typhoon, earthquake | KO | key | ⚠️ unverified (KR-only portal) | free | REST |
| [KOSIS Statistics (국가통계포털)](https://kosis.kr/eng/) | Official national statistics, 226 categories, English browse | EN~ | key | ❌ Korean phone + citizenship required (confirmed) | free | SDK |
| [Seoul Open Data Plaza](https://data.seoul.go.kr) | Seoul municipal data: real-time bus, subway, Wi-Fi, parking | KO | key | ⚠️ unverified | free | REST |
| [PublicDataReader](https://github.com/WooilJeong/PublicDataReader) | Python library wrapping data.go.kr + KOSIS + ECOS (tool, not an API) | KO | none | ✅ pip install (key gates still apply) | free | SDK |

<sub>[↑ back to top](#contents)</sub>

---

## 🛒 Commerce & Logistics

Selling physical goods or building on a Korean storefront. Note the entity wall: domestic Coupang and Naver SmartStore need a Korean business, but Coupang's global program does not.

| Service | What you get | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
|---|---|---|---|---|---|---|
| [Cafe24 REST API (카페24)](https://developers.cafe24.com/docs/en/api/) | Full store API (products, orders, customers, inventory); ~2M stores | EN | oauth | ✅ foreign developer registration | free | REST |
| [Coupang Global Sellers](https://globalsellers.coupang.com/en/) | Cross-border selling on Coupang, ship from home country | EN | key | ✅ no Korean entity required | free | REST |
| [Coupang Open API (domestic)](https://developers.coupangcorp.com/hc/en-us) | Product/order/shipment for a domestic Coupang seller account | EN | key | ❌ Korean legal entity required | free | REST |
| [Naver Commerce API (SmartStore)](https://github.com/commerce-api-naver/commerce-api) | Order/product/seller management for SmartStore | KO | oauth | ❌ Korean business + bank account | free | REST |
| [Imweb Open API (아임웹)](https://developers-docs.imweb.me/) | Order/product/member data for Imweb stores | KO | key | ⚠️ unverified (KR-only console) | free | REST |
| [AfterShip (Korea carriers)](https://www.aftership.com/tracking-api) | Unified tracking for Korea Post, CJ, Lotte + 1,200 global carriers | EN | key | ✅ self-serve, free tier | freemium | REST |
| [SweetTracker / SmartParcel (스마트택배)](https://info.sweettracker.co.kr/apidoc) | Tracking API across 20+ Korean couriers | KO | key | ⚠️ unverified (email application) | freemium | REST |
| [Goodsflow (굿스플로)](https://www.goodsflow.io/api) | Standardized tracking for 20+ domestic + international couriers | EN~ | key | ⚠️ partnership, ~2-week setup | paid | REST |

<sub>[↑ back to top](#contents)</sub>

---

## ⚖️ Compliance Gotchas

Not pluggable APIs, but the legal tripwires most likely to surprise a foreign builder. Verify against the official source before relying on any of these.

- **Google Maps is restricted by law.** The National Geospatial Intelligence Act limits export of high-resolution map data, so Google disabled turn-by-turn and detailed mapping in Korea. Use Kakao or Naver, which licensed the government data. (See [Maps](#️-maps--location).)
- **[PIPA](https://www.pipc.go.kr/eng/) applies even with no Korean office** if you provide goods/services to Korean users. Requires a Korean-language privacy policy, separate (unbundled) consent per purpose, a retention/destruction schedule, and 72-hour breach notification. ([PIPA in English](https://elaw.klri.re.kr/eng_service/lawView.do?hseq=62389&lang=ENG))
- **Cross-border data transfer needs consent.** Under PIPA, transferring Korean users' personal data abroad needs separate consent unless the destination has a PIPC adequacy decision. Remote DB access by an overseas team counts as a transfer.
- **The Location Information Act (위치정보법) gates location services.** Collecting or routing personal location data requires KCC registration; offering a location-based service requires KCC reporting. Most foreign startups don't know this law exists. ([English text](https://elaw.klri.re.kr/eng_service/lawView.do?hseq=43349&lang=EN))
- **The Network Act (정보통신망법) triggers ISMS-P at scale.** ISMS-P certification (KISA) becomes mandatory around 1M daily Korean users or ~₩10B Korean revenue; a Korean domestic agent is required above certain thresholds. *(Verify current thresholds against [law.go.kr](https://law.go.kr) before relying.)*
- **Under-14 users need verifiable guardian consent** (PIPA Art. 22). The 2007 internet real-name system was struck down in 2012; don't confuse it with today's 본인인증 regime.
- **A joint certificate (공동인증서) is still needed for some government portal integrations** (Hometax, etc.). Issuing one as a foreigner requires an ARC or Korean business registration.

<sub>[↑ back to top](#contents)</sub>

---

## Related lists

Part of Seoulstart's Korea list family:

- [Awesome Living in Korea](https://github.com/seoulstart/awesome-living-in-korea#readme) — for foreign residents: visas, housing, healthcare, taxes, work.
- [Awesome Korea Travel](https://github.com/seoulstart/awesome-korea-travel#readme) — for visitors: trip planning, transit, cities, things to do.

Other focused lists worth a look:

- [public-apis-4Kr](https://github.com/yybmion/public-apis-4Kr) — broad catalog of APIs available for Korean services.
- [awesome-mcp-korea](https://github.com/darjeeling/awesome-mcp-korea) — full catalog of MCP servers for the Korean market.

## Contributing

Contributions welcome. See [CONTRIBUTING.md](CONTRIBUTING.md). Every entry must be a resource a builder can actually plug in, and must carry honest foreigner-access annotations. **Do not guess the 🛂 rating.** If you have not confirmed it from official docs or a real signup attempt, mark it `⚠️ unverified`. A wrong ✅ wastes a builder's day.

This list makes no guarantee about the accuracy, security, or current availability of any linked resource. Access rules, pricing, and APIs change. Verify before you build.

## License

[CC0](LICENSE): to the extent possible under law, the curation in this list is dedicated to the public domain. Linked resources retain their own licenses.

---

Maintained by [Seoulstart](https://seoulstart.com).
