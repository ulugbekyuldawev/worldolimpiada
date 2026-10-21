# Render'ga joylash

## 1-usul: Blueprint (eng oson)
1. Loyihani GitHub'ga yuklang (fayllar repozitoriyaning eng yuqorisida bo'lsin: `main.py`, `render.yaml`, `tests/` ...).
2. https://dashboard.render.com → **New → Blueprint** → GitHub repozitoriyangizni tanlang.
3. Render `render.yaml` ni o'qib, 2 ta narsa yaratadi: `olimpiada-bot` (bot) va `olimpiada-db` (PostgreSQL).
4. Render so'raganda kiriting:
   - `BOT_TOKEN` — BotFather tokeni
   - `ADMIN_PASSWORD` — admin paroli
5. **Apply** ni bosing. Deploy tugagach, Logs'da `Olimpiada bot ishga tushdi. Versiya: ...` chiqadi.
6. Botga `/versiya` yozing — yangi versiya javob beradi.

## 2-usul: Qo'lda
1. **New → PostgreSQL** → nom bering → Create. Yaratilgach, **Internal Database URL** ni nusxalang.
2. **New → Web Service** → GitHub repozitoriyani tanlang:
   - Runtime: **Python 3**
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `python main.py`
   - Instance Type: Free (yoki pullik)
3. **Environment** bo'limiga qo'shing:
   ```
   BOT_TOKEN=...
   ADMIN_LOGIN=admin
   ADMIN_PASSWORD=...
   DATABASE_URL=<Internal Database URL>
   TIMEZONE=Asia/Tashkent
   PYTHON_VERSION=3.12.7
   ```
4. **Create Web Service**.

## Bepul tarif haqida MUHIM
- **Bot uxlab qolmasligi uchun:** bepul Web Service 15 daqiqa davomida unga hech kim murojaat qilmasa "uxlaydi" va bot javob bermay qo'yadi.
  Buning oldini olish uchun https://uptimerobot.com da bepul monitor yarating:
  Monitor Type: **HTTP(s)**, URL: `https://<sizning-servis-nomingiz>.onrender.com/`, Interval: **5 minutes**.
  Bot shu manzilda `OK ...` deb javob beradi va uyg'oq turadi.
- **Bepul PostgreSQL 30 kundan keyin o'chadi** (Render qoidasi). Olimpiadadan keyin natijalarni Excel'da yuklab oling
  yoki bazani pullik tarifga o'tkazing. Muddatsiz bepul baza kerak bo'lsa, Neon (neon.tech) yoki Supabase'dan
  PostgreSQL olib, uning manzilini `DATABASE_URL` ga qo'yish mumkin.
- Bot faqat **bitta** joyda ishlashi kerak. Render'ga o'tgach, Railway'dagi eski botni o'chiring (bitta tokenda ikkita bot bir-biriga xalaqit beradi).
