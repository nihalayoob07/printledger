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
| 🔄 **Sync (optional)** | Connect your own Firebase project, pair devices with a shared code |
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

Sync runs on **your own** Firebase project. Nothing is bundled in this file, so your data never touches anybody else's database, including mine. Skip the whole section and the calculator, ledger, and bills work exactly the same.

1. Create a free project at [firebase.google.com](https://firebase.google.com).
2. Build → **Realtime Database** → Create Database.
3. Project settings → Your apps → **Web** → copy the config snippet.
4. In the app: **Settings → Sync** → paste the snippet → **Connect a project**.
5. **Generate a code**, then **Connect**. Put the same code into the app on your other device.

The config is saved in `localStorage`, not in the file, so re-downloading `index.html` never clobbers it.

### ⚠️ Set the database rules

The sync code is the only credential. Leave the database in test mode and anyone who finds your project URL can read and write everything in it.

Realtime Database → **Rules**:

```json
{
  "rules": {
    "syncedUsers": {
      "$code": {
        ".read": "$code.length >= 20",
        ".write": "$code.length >= 20 && newData.hasChild('settings')"
      }
    }
  }
}
```

Your data lives under a long random code that acts as the key, and short or guessable codes are refused outright. Use the generated one — the app won't accept anything under 16 characters. Treat it like a password, because that's what it is.

Being straight about the limits: anyone holding the code has full access, there's no per-user login, and there's no audit trail. That's a fair trade for one person syncing two devices. If you have staff, or customer data you're legally responsible for, put Firebase Authentication in front of it.

## 🎨 Customizing

It's one file — everything's in `index.html`. Good starting points:

| Want to change... | Look for... |
|---|---|
| Colors / themes | `:root` and `[data-theme="..."]` blocks in `<style>` |
| Default rates | the `defaults` object in the script |
| Default coupons | the `defCoupons` array |
| Currency (currently ₹ / INR) | search for `inr(` and `en-IN` |
| Sync target | nothing to edit — paste your Firebase config in **Settings** |

## 📄 License

MIT — see [LICENSE](LICENSE). Use it, modify it, sell prints priced by it, whatever — just keep the copyright notice so credit stays attached.

---

<div align="center">
<sub>Made by Nihal, for pricing 3D prints without doing the math by hand every time.</sub>
</div>
