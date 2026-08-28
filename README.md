# 📚 Kutubxona Bot

Kitob nomini yozing — bot qaysi javon va qatorda ekanini topib beradi.
Ma'lumotlar SQLite faylida, Railway Volume ichida doimiy saqlanadi.

## Railway'ga deploy qilish

1. Bu fayllarni GitHub repozitoriyingizga yuklang (app.py, requirements.txt, Procfile).
2. Railway'da yangi loyiha yarating, GitHub repo'ni ulang.
3. **Volume qo'shish** (bu — doimiy xotira, juda muhim qadam!):
   - Loyiha ichida servisingizni tanlang → **Settings** → **Volumes** → "New Volume"
   - **Mount Path** ni aynan `/data` deb yozing
   - Saqlang
4. **Variables** boʻlimiga quyidagilarni qoʻshing:
   - `BOT_TOKEN` — @BotFather'dan olingan token
   - `ADMIN_IDS` — sizning Telegram user ID'ingiz (vergul bilan bir nechta bo'lishi mumkin: `123456789,987654321`). O'z ID'ingizni @userinfobot orqali bilib olasiz.
   - `WEBHOOK_URL` — hozircha bo'sh qoldiring
5. **Settings** → **Networking** → "Generate Domain" bosing — sizga domain beriladi (masalan `kutubxona-bot-production.up.railway.app`)
6. Shu domenni `https://` bilan boshlab, **Variables**'dagi `WEBHOOK_URL` ga qo'shing
7. O'zgarish saqlangach, Railway avtomatik qayta deploy qiladi (1-2 daqiqa kuting)
8. Brauzerda shu manzilga bir marta kiring: `https://SIZNING-DOMAIN.up.railway.app/set_webhook`
9. Botga /start yozing.

## Excel formati (ommaviy yuklash uchun)

1-qator sarlavha, keyingi qatorlarda ma'lumot:

| Nomi | Muallif | Javon | Qator | Soni |
|---|---|---|---|---|
| O'tkan kunlar | Abdulla Qodiriy | 3 | 2 | 5 |
| Sarob | Cho'lpon | 3 | 2 | 2 |
| Kecha va kunduz | Abdulla Qahhor | 1 | 4 | 3 |

- Javon va Qator — albatta butun son.
- Soni — ixtiyoriy, bo'sh qoldirsa ham bo'ladi.

## Qanday ishlaydi

- Oddiy foydalanuvchi kitob nomini (yoki muallifni) yozadi → bot bazadan qisman moslikda (nomning bir qismi ham yetarli) qidiradi va javon/qatorni chiqaradi.
- Admin (`ADMIN_IDS` ro'yxatidagi kishi) uchun qo'shimcha tugmalar chiqadi:
  - **➕ Kitob qo'shish** — bosqichma-bosqich (nom → muallif → javon → qator → soni)
  - **📂 Excel yuklash** — .xlsx faylni to'g'ridan-to'g'ri botga yuborsa, avtomatik bazaga qo'shiladi
  - **📋 Javon bo'yicha ko'rish** — javon raqamini kiritsa, o'sha javondagi barcha kitoblar qatorlar bo'yicha guruhlangan holda chiqadi
  - **📊 Statistika** — jami kitoblar va javonlar soni

## Muhim: Volume haqida

Ma'lumotlar `/data/kutubxona.db` faylida saqlanadi. Agar Volume qo'shishni unutsangiz, Railway konteynerni qayta ishga tushirganda barcha kitoblar o'chib ketadi. Shuning uchun 3-qadamni albatta bajaring — bepul rejada ham Volume mavjud (odatda ~0.5-1 GB gacha bepul, bu minglab kitob uchun yetarli).
