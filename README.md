<div align="center">

# 🖨️ The Print Vault

**Price your 3D prints. Track what you've sold. Bill your customers.**
A single HTML file. No backend. No build step. No dependencies to install.

![No build step](https://img.shields.io/badge/build-none-C6F24A?style=flat-square)
![Zero dependencies](https://img.shields.io/badge/dependencies-zero-74E3A3?style=flat-square)
![Storage](https://img.shields.io/badge/storage-localStorage-38D9F0?style=flat-square)
![License: MIT](https://img.shields.io/badge/license-MIT-FF8A3D?style=flat-square)
![Themes](https://img.shields.io/badge/themes-5-A78BFA?style=flat-square)

</div>

---

Built to run the pricing, sales log, and billing for a 3D printing side business — but the model (material + power + labour + margin → price) works for any per-item, cost-plus-margin business. Fork it, reskin it, make it yours.

## ✨ Features

| | |
|---|---|
| 🧮 **Press** | Enter weight + print time → instant price, live as you type |
| 📒 **Ledger** | Every priced job gets logged — cost, profit, and margin per entry |
| 🧾 **Bills** | Group ledger entries into a bill, apply a coupon, export as a PNG image |
| 🎟️ **Coupons** | Save reusable % discount codes, apply at pricing or billing |
| 📤 **CSV export** | Dump the whole ledger to CSV whenever you want |
| 🔄 **Sync (optional)** | Pair two devices with a shared code, data syncs live via Firebase |
| 🎨 **5 themes** | Obsidian, Aurora, Sunset, Ocean, and Paper (light mode) |
| 📱 **Mobile-first** | Built for one-handed use on the shop floor, scales up to desktop |

## 🧠 How the pricing works

```
filament cost   =  (weight in grams ÷ 1000)  ×  filament cost per kg
power cost      =  (printer watts ÷ 1000)    ×  print hours  ×  electricity rate
labour cost     =  print hours               ×  labour rate per hour
packaging cost  =  flat fee, if toggled on

subtotal        =  filament + power + labour + packaging
profit          =  subtotal × your profit %
price           =  subtotal + profit,  minus any coupon %
```

Every rate is yours to set — nothing is hardcoded to make sense for anyone but you.

## 🚀 Getting started

```bash
git clone <this-repo>
```

1. Open `index.html` in a browser. That's the whole install.
2. Open **Settings** (⚙️ icon) and enter your own rates — filament ₹/kg, printer watts, electricity rate, labour rate, packaging fee, profit %.
3. Price a print, hit log, and it lands in your Ledger.

**On your phone:** host the file somewhere static (GitHub Pages, Netlify, or just email it to yourself), open it in mobile Chrome/Safari, and add it to your home screen for a full app feel.

## 🔒 Data & privacy

Everything lives in your browser's `localStorage`. Nothing leaves your device unless you deliberately turn on sync. No server, no analytics, no accounts.

## 🔄 Cross-device sync (optional)

Sync uses Firebase Realtime Database so your data can follow you between devices.

> [!IMPORTANT]
> The Firebase project wired into this file is **mine**. If you fork this and turn sync on without swapping the config, you'll be syncing into *my* database. Set up your own first:

1. Create a free project at [firebase.google.com](https://firebase.google.com).
2. Enable **Realtime Database**.
3. Replace the `fbConfig` object near the top of the `<script>` block in `index.html` with your own project's config.

Skip this and sync just fails quietly (offline) — the calculator, ledger, and bills all work fine without it.

## 🎨 Customizing

It's one file — everything's in `index.html`. Good starting points:

| Want to change... | Look for... |
|---|---|
| Colors / themes | `:root` and `[data-theme="..."]` blocks in `<style>` |
| Default rates | the `defaults` object in the script |
| Default coupons | the `defCoupons` array |
| Currency (currently ₹ / INR) | search for `inr(` and `en-IN` |

## 📄 License

MIT — see [LICENSE](LICENSE). Use it, modify it, sell prints priced by it, whatever — just keep the copyright notice so credit stays attached.

---

<div align="center">
<sub>Made by Nihal, for pricing 3D prints without doing the math by hand every time.</sub>
</div>
