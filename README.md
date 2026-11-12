# 🤖 𝐌𝐄𝐃𝐔𝐒𝐀 𝐋𝐈𝐊𝐄 𝐁𝐎𝐓 — Premium Dual-API Edition

Telegram-এর জন্য premium like bot। দুইটি আলাদা API একসাথে চলে:

- 💎 **100-Like-API** → `/premium` (BD server, community-gated)
- 🌐 **Public-Like-API** → `/like <uid>` (BD server, force-join gated, **যেকোনো গ্রুপে চলবে**)
- ➕ **Add-to-Group** → বটের প্রতিটি মেসেজের নিচে বাটন, পাবলিক নিজের গ্রুপে বট অ্যাড করতে পারবে

---

## ✨ Features

### 💎 100-Like Bot (Bot 1)
- BD region fixed like (100 likes)
- Community gating (allowed group/channel member হতে হবে)
- VIP system (1/day or unlimited)
- Daily limit (configurable)
- Auto-pin on open/close

### 🌐 Public-Like Bot (Bot 2)
- BD server like (`/like <uid>`)
- যেকোনো গ্রুপে অ্যাড করে ব্যবহার করা যায় (`/public_mode public`)
- বট গ্রুপে অ্যাড হলে auto welcome + admin-কে নোটিফিকেশন
- Force-join gating (multi group + channel)
- Ban/unban system
- VIP 3/day
- Inline join buttons

### 🔗 Shared (Premium)
- Premium formatted messages with decorative fonts
- Inline admin panel
- BD timezone (Asia/Dhaka, UTC+6) — midnight reset at 12:00 AM
- Per-API stats tracking
- Dual state files (independent config per API)
- 🎉 reaction on success
- Dynamic next-reset timer

---

## 📋 Requirements

- **Python** 3.10 or higher
- **Telegram Bot Token** (from [@BotFather](https://t.me/BotFather))
- **Two like APIs** (URL + key for each)
- **Your Telegram user ID** (from [@userinfobot](https://t.me/userinfobot))

---

## 🚀 Setup

### 1. Clone / download ফোল্ডার

সব ফাইল একই ফোল্ডারে রাখুন:

```
medusa-like-bot/
├── bot.py
├── .env
├── requirements.txt
├── 100like_state.json
├── public_state.json
└── README.md
```

### 2. Virtual environment (recommended)

```bash
python -m venv venv
# Linux/Mac
source venv/bin/activate
# Windows
venv\Scripts\activate
```

### 3. Dependencies install

```bash
pip install -r requirements.txt
```

### 4. `.env` configure

`.env.example` → `.env` rename করুন, তারপর ভিতরে বসান:

```env
BOT_TOKEN=your_bot_token_from_botfather
ADMIN_IDS=your_telegram_id
ADMIN_2_ID=other_admin_telegram_id

API_1_URL=https://your-api.com/
API_1_KEY=your_key
# API_2..API_4 একই ভাবে (ক্রমান্বয়ে চেষ্টা হয়)
```

> ⚠️ **গুরুত্বপূর্ণ:** `API_100_LIKE_URL` এবং `API_PUBLIC_LIKE_URL` শেষে `/` থাকা ভালো (না থাকলেও bot normalize করে নেয়)।

### 5. Bot কে admin করুন

Force-join এর জন্য bot কে নিচের জায়গায় **admin** করতে হবে:

- ✅ Force-join group
- ✅ Force-join channel
- ✅ Allowed group

**Permission দর্বণ:** `Ban users` + `Invite users via link` + `Pin messages` (auto-pin এর জন্য)

### 6. Bot চালান

```bash
python bot.py
```

সফল হলে দেখবেন:
```
✅ 100-like-API: https://...
✅ public-like-API: https://...
⏰ Midnight reset (BD) scheduled
🤖 Bot running — dual API mode
```

---

## 👑 এডমিন সেটআপ

`.env`-তে দুইটা ঘর আছে:

```env
ADMIN_IDS=111111111      # মূল এডমিন (সব কমান্ড)
ADMIN_2_ID=222222222     # আরেকজন এডমিন
```

আরেকজন এডমিন বটে হুবহু এডমিনের মতই দেখবেন (একই প্যানেল, একই লিমিট-ছাড়া ব্যবহার, একই কমান্ড),
শুধু এই কমান্ডগুলো তাঁর জন্য কাজ করবে না (বট চুপ থাকবে, কোনো মেসেজ দেবে না) এবং `/help`-এও দেখাবে না:

`/add_group` `/ban_add_group` `/add_channel` `/ban_add_channel` `/premium_allow` `/public_bot_allow`
`/Bend_group` `/Bend_group_id` `/Unblock_group_id`

এছাড়া API-র URL, বট অ্যাড/রিমুভ নোটিফিকেশন ও ডেইলি রিপোর্ট শুধু মূল এডমিন পান।

---

## 🎛️ Commands

### 👤 সবার জন্য
`/start` `/help` `/myinfo` `/id` `/tg_id` `/top` `/like <uid>` `/like <region> <uid>` `/premium <uid>`

### 👑 এডমিন
| Command | কাজ |
|---|---|
| `/admin` `/stats` `/user_like` `/api` | প্যানেল ও স্ট্যাটস |
| `/api_check` | ৪টি API সার্ভার লাইভ চেক |
| `/backup` | ডাটা ফাইল ইনবক্সে ব্যাকআপ |
| `/premium_bot_open` `/premium_bot_off` | Premium (আগের 100-like) চালু/বন্ধ |
| `/max_like_on` `/max_like_off` | MAX Like চালু/বন্ধ; গ্রুপে status message pin |
| `/public_bot_on` `/public_bot_off` | পাবলিক বট চালু/বন্ধ |
| `/public_mode public\|private` | যেকোনো গ্রুপে / শুধু allowed গ্রুপে |
| `/groups` | বট যেসব গ্রুপে আছে |
| `/setlimit_premium <n>` `/setlimitpub <n>` | ডেইলি লিমিট |
| `/VIP <id> <limit>` `/banvip <id>` `/vip_list` | VIP |
| `/ban_user <id>` `/unban_user <id>` | ইউজার ব্যান (রিপ্লাই দিয়েও হয়) |
| `/set_photo_like_ms` `/remove_photo` | লাইক মেসেজের ছবি (ছবির caption-এও চলে) |
| `/broadcast` `/cancel` | সব গ্রুপে মেসেজ |
| `/blocked_groups` | ব্লকড গ্রুপ লিস্ট |
| `/like_bot_mute` | যে গ্রুপে দেবেন সেখানে বট থাকবে কিন্তু কোনো মেসেজ/রিয়্যাকশন দেবে না (কমান্ডও কাজ করবে না) |
| `/like_bot_unmute` | ওই গ্রুপে আবার চালু |
| `/muted_groups` | মিউট করা গ্রুপের লিস্ট |

### 🔒 শুধু মূল এডমিন
`/add_group` `/ban_add_group` `/add_channel` `/ban_add_channel` `/premium_allow` `/public_bot_allow` `/Bend_group` `/Bend_group_id` `/Unblock_group_id`

---

## 📊 State Files

বট তার সব data JSON ফাইলে রাখে:

### `100like_state.json`
```json
{
  "config": { "status": "on", "public": false, "limit": 2 },
  "groups": {},
  "channels": {},
  "vip": {},
  "users": {},
  "stats": {}
}
```

### `public_state.json`
```json
{
  "config": { "status": "on", "mode": "public", "limit": 1 },
  "groups": {},
  "force_join": { "groups": [], "channels": [] },
  "vip": {},
  "banned": {},
  "users": {},
  "stats": {}
}
```

> 💡 **Backup:** যেকোনো সময় এই দুই JSON ফাইলের copy রাখলে সব data রক্ষা পাবে। Restore করতে চাইলে ফাইল দুটো replace করে bot restart দিন।

---

## 🌏 Timezone

Bot **Bangladesh time (UTC+6)** ব্যবহার করে:

- 🕛 Daily reset: **12:00 AM (BD)**
- ⏰ User limit reset: প্রতিদিন রাত ১২টায়
- 📅 Stats date: BD date অনুযায়ী

---

## 🔒 Security Notes

- ⚠️ `.env` ফাইল **কখনো** GitHub-এ push করবেন না
- ⚠️ `BOT_TOKEN` কারো সাথে শেয়ার করবেন না
- ⚠️ `ADMIN_IDS` শুধু বিশ্বস্ত user-এর ID দিন
- ⚠️ API keys কখনো hardcode করবেন না — সবসময় `.env`-এ রাখুন

**`.gitignore`-এ রাখুন:**
```
.env
bot.log
__pycache__/
venv/
```

---

## 🛠️ Troubleshooting

### ❌ Bot চালু হচ্ছে না
- `BOT_TOKEN` ঠিক আছে কিনা চেক করুন
- Python version 3.10+ কিনা দেখুন
- `pip install -r requirements.txt` আবার চালান

### ❌ `/premium` কাজ করছে না
- `/api` কমান্ড দিয়ে দেখুন 100-Like-API `✅ Ready` কিনা
- `.env`-এ `API_100_LIKE_URL` এবং `API_100_LIKE_KEY` সঠিক কিনা যাচাই করুন
- Server online আছে কিনা দেখুন

### ❌ Force-join কাজ করছে না
- Bot কে force-join group/channel-এ **admin** করুন
- Invite link valid কিনা দেখুন
- `/public_like_add_group @username` আবার চালান

### ❌ `Chat not found` error
- Bot কে গ্রুপ/চ্যানেলে add + admin করুন
- গ্রুপ/চ্যানেল private হলে bot-কে আগে member করতে হবে

### ❌ Reset হচ্ছে না
- Bot server এর clock ঠিক আছে কিনা দেখুন
- `bot.log`-এ `✅ Daily reset at ...` আছে কিনা দেখুন

---

## 📂 File Structure

```
medusa-like-bot/
├── bot.py                    ← মূল bot logic
├── .env                      ← secrets (token, keys)
├── .env.example              ← template (আসল কী এখানে রাখবেন না)
├── requirements.txt          ← Python packages
├── README.md                 ← this file
├── 100like_state.json        ← Bot 1 state
├── public_state.json         ← Bot 2 state
└── bot.log                   ← auto-generated logs
```

---

## 🎯 Quick Start Checklist

- [ ] Python 3.10+ install
- [ ] ফোল্ডার তৈরি + সব ফাইল রাখা
- [ ] `pip install -r requirements.txt`
- [ ] `.env` file তৈরি + token + API URLs + admin ID
- [ ] Bot কে force-join group/channel-এ admin করা
- [ ] `python bot.py` চালানো
- [ ] `/api` দিয়ে দুই API ✅ চেক
- [ ] `/open_100like_bot` + `/public_bot_on` দিয়ে bot চালু
- [ ] `/admin` দিয়ে panel দেখে নিশ্চিত হওয়া

---

## 📝 License

Private bot. Authorized user-দের জন্য। Redistribution নিষিদ্ধ।

---

## 💬 Support

সমস্যা হলে `bot.log` ফাইল দেখুন। Log-এ প্রতি API call, error, reset সব থাকে।

---

**Built with ❤️ for Telegram**

---

## 🎁 Referral System (নতুন)

| কমান্ড | কে ব্যবহার করবে | কাজ |
|---|---|---|
| `/myrefer` | সবাই | নিজের রেফার লিংক + প্রোফাইল + মোট রেফার |
| `/leaderboard` | সবাই | রেফার লিডারবোর্ড (সবচেয়ে বেশি রেফারকারী টপে, টপ ১০ + নিজের র‍্যাংক) |
| `/all_user_refer` | এডমিন (ইনবক্সে) | সবার রেফার লিস্ট (Telegram ID সহ); ১০+ হলে `refer_10plus.json` ফাইল |
| `/med_x <id> <n>` | এডমিন | রেফার ঠিক `n` করো |
| `/med_x <id> +n` / `-n` | এডমিন | রেফার বাড়াও / কমাও |

- লিংক: `https://t.me/<BOT>?start=ref_<telegram_id>`
- শুধু **নতুন** ইউজার কাউন্ট হয় (আগের ইউজার ও নিজে নিজের লিংকে কাউন্ট হয় না), এবং ফোর্স-জয়েন পূরণ করার পর।
- প্রতিটি রেফারে মালিকের কাছে নোটিফিকেশন যায়।
- কেউ ১০ রেফার পূর্ণ করলে মালিকের কাছে নাম, ইউজারনেম, Telegram ID, প্রোফাইল লিংক ও "Open Profile" বাটন সহ নোটিফিকেশন যায় (একবারই)।
- বটের প্রতিটি মেসেজের নিচে `👑 OWNER` বাটন থাকে → https://t.me/HAFSAN_KUN
- ডেটা ফাইল: `referrals.json`, `refer_10plus.json` (`/backup` এ আসবে)
- `REFER_GOAL = 10` — bot.py তে বদলানো যায়।

---

## 🛍 MyShop (আপডেট)

| আইটেম | দাম |
|---|---|
| ➕ +1 Daily Like Limit | **2 coins** (আগে 1) |
| ⚡ 7 Days Auto Like | **7 coins** (আগে 10) |

- ⚡ **Auto Like কেনা যাবে শুধু মেইন বটে → [@MEDUSA_LIKE_BoT](https://t.me/MEDUSA_LIKE_BoT)**
  অন্য বটে Auto Like বাটনে চাপ দিলে সরাসরি মেইন বটে পাঠিয়ে দেবে।
- মেইন বট চেনা হয় `MAIN_BOT_USERNAME` দিয়ে (ডিফল্ট `MEDUSA_LIKE_BoT`, `.env`-এ বদলানো যায়)।
- 🛍 Shop মেসেজের নিচে **👑 OWNER** বাটন আসে না।
- দাম বদলাতে `bot.py`-তে `SHOP_LIMIT_PRICE` ও `SHOP_AUTO_PRICE` দেখুন — একই ফাইল সব বটে চলে বলে সব বটে একই দাম।

## 💰 /bal — কয়েন ব্যালেন্স ও গিফট

- `/bal` → নিজের কয়েন দেখায়।
- কারো মেসেজে **রিপ্লাই দিয়ে `/bal`** → তার কয়েন দেখায় (রেফার, গিফট, খরচসহ)।
- **শুধু এডমিনের** মেসেজে `🎁 Gift Coins` বাটন আসে → চাপ দিয়ে সংখ্যা লিখলে সেটাই ওই ইউজারের কয়েনে যোগ হয় (ইউজারকে নোটিফিকেশনও যায়)। বাতিল: `/cancel`
- গিফট `shop.json`-এ `gift` ফিল্ডে সেভ হয়। কয়েন = রেফার + গিফট − খরচ।

## 📈 Daily Limit — বাড়তে থাকা দাম

+1 Daily Like Limit-এর দাম প্রতিবার ১ coin করে বাড়ে: ১ম বার **2**, ২য় বার **3**, ৩য় বার **4**, ৪র্থ বার **5** … (দাম = 2 + এ পর্যন্ত কেনা limit সংখ্যা)। শপের বাটন ও লেখায় সবসময় পরের দাম দেখায়।

## 🎫 লাইক মেসেজে ডেইলি লিমিট

প্রতিটি সফল লাইক মেসেজের নিচে ইউজারের লিমিট দেখায়: Used / Left / Total + প্রগ্রেস বার।
এডমিনের (মালিকের) জন্য দেখায় **♾ ∞ UNLIMITED**। `/like` ও `/premium` — দুই জায়গাতেই কাজ করে।

## 🪙 Coin Store

`/myrefer` ও `/myshop` — দুই জায়গাতেই **🪙 Buy Coins** বাটন আছে। চাপ দিলে MEDUSA COIN STORE-এর প্রাইস লিস্ট দেখায় (১ coin = ৳১০ = ১৭০+ Like … ১০০ coin = ৳১০০০)। লিস্টের নিচে শুধু একটাই **🛒 BUY COINS** বাটন → https://t.me/HAFSAN_KUN (আর কোনো বাটন নেই)।
লিস্ট বদলাতে `bot.py`-তে `COIN_STORE_TEXT` দেখুন।


## ⚡ MAX Like Mode (নতুন)

- Owner গ্রুপে `/max_like_on` দিলে MAX Like Mode চালু হবে এবং ঘোষণা pin করার চেষ্টা করবে।
- চালু থাকা অবস্থায় ইউজাররা `/max <uid>` ব্যবহার করতে পারবে। উদাহরণ: `/max 12345678`।
- Owner `/max_like_off` দিলে ফিচার বন্ধ হবে এবং বন্ধের ঘোষণাও pin করার চেষ্টা করবে।
- এই ফিচারের API আলাদা: `.env`-এ `MAX_API_URL` ও `MAX_API_KEY` দিতে হবে। API-টি `GET <MAX_API_URL>/like` এবং `key`, `uid`, `server_name` parameter গ্রহণ করবে; response-এ `status`, `LikesGivenByAPI`, `PlayerNickname`, `LikesbeforeCommand`, `LikesafterCommand` থাকতে হবে।
- Bot-কে গ্রুপে Pin Messages permission দিতে হবে। চালু/বন্ধ অবস্থা `max_like_state.json`-এ সংরক্ষিত থাকে।
