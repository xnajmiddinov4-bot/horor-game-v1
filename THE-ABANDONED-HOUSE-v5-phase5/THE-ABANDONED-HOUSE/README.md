# THE ABANDONED HOUSE

## Ishga tushirish
1. ZIP arxivni Extract qiling.
2. `the-abandoned-house` papkasini VS Code da oching.
3. VS Code Live Server kengaytmasi orqali `index.html` ni oching.
4. Internet yoqilgan bo‘lsin: Three.js CDN orqali yuklanadi.
5. BOSHLASH tugmasini bosing. Agar mouse lock ruxsati chiqmasa, o‘yin maydonini bosing. WASD bilan yurish, F fonar, E buyum/eshik, Shift tez yurish.

Eslatma: Three.js CDN ishlatilgani uchun birinchi yuklashda internet kerak.

## Tuzatishlar (FIXED)
- Asosiy xato: `game.js` da arvoh (ghost) modeli `Object.assign(mesh,{position:...})` bilan yaratilgan edi. Three.js r128 da `position` faqat o'qiladigan xossa, shuning uchun skript shu joyda TypeError bilan to'xtab, BOSHLASH tugmasi hech qachon ulanmagan. Endi `position.set(...)` ishlatiladi.
- Xatoliklar ekranda tushunarli xabar bilan chiqadi (WebGL, Three.js, game.js yuklanmasa yoki boshqa JS xatosi).
- Three.js yuklash tartibi: `lib/three.min.js` → cdnjs → jsDelivr → unpkg.
- O'yin yuklanib bo'lmasdan BOSHLASH bosilsa, tayyor bo'lgach avtomatik boshlanadi.
- Sensorli ekranli noutbuklarda sichqoncha bilan qarash endi ishlaydi (faqat telefon/planshet "touch" rejimida).
- E/F tugmasi ushlab turilganda qayta-qayta ishlamaydi; HUD yozuvlari sichqoncha bosishini to'smaydi.

## YANGILANISH 1: MONSTER AI
- Uyda maxluq paydo bo‘ladi (o‘yin boshlangach ~18 soniyada, o‘yinchidan uzoq joyda).
- Holatlar: **Patrul** (uyni aylanadi, ba’zan o‘yinchi tomon “pusadi”) → **Tekshirish** (shovqinni eshitadi) → **Quvish** (ko‘rsa) → **Qidirish** (yo‘qotsa oxirgi ko‘rilgan joyga boradi).
- Shovqin: yugurish (uzoqqa eshitiladi), yurish (yaqinga), eshik ochish, kalit olish, qulfli eshikni urish.
- Ko‘rish: fonar yoqiq bo‘lsa ~14 m, o‘chiq bo‘lsa ~6 m; devor va yopiq eshik to‘sadi.
- Yo‘l topish: xonalar/eshiklar bo‘yicha waypoint grafi + eng qisqa yo‘l; eshiklarni o‘zi ochadi (chiqish eshigidan o‘ta olmaydi).
- Tezlik: patrul 1.3, tekshirish 1.9, quvish 3.0+ (kalit sayin tezlashadi). O‘yinchi: yurish 2.3, yugurish 4.4.
- Tovush: fazoviy qadam tovushlari, hurillash, yurak urishi; yaqinlashganda ekran qizaradi.
- Ushlasa: “SIZNI USHLASHDI” ekrani va qayta urinish.

## YANGILANISH 3 (1-bosqich): 2 o‘yinchi lobbisi
- Menyu: YAKKA O‘YIN / MULTIPLAYER. MULTIPLAYER → XONA YARATISH (host kod oladi) yoki XONAGA QO‘SHILISH (kodni kiriting).
- Aloqa: PeerJS (WebRTC), signal uchun ochiq PeerJS Cloud, STUN bilan. TURN yo‘q — ba’zi tarmoqlarda to‘g‘ridan-to‘g‘ri ulanish bo‘lmasligi mumkin (`multiplayer.js` boshidagi `ICE` ro‘yxatiga o‘z TURN serveringizni qo‘shishingiz mumkin).
- PeerJS: `lib/peerjs.min.js` → jsDelivr → unpkg tartibida yuklanadi.
- Hozir sinxron: o‘yinchi joyi, qarash yo‘nalishi, yurish/yugurish animatsiyasi, fonar. **Hali sinxron emas:** maxluq (multiplayerda vaqtincha o‘chirilgan), kalitlar, eshiklar — 2-bosqichda.
- Host brauzeri fonga o‘tsa yoki sahifa yangilansa, xona yopiladi.

## YANGILANISH 4 (1–3-bosqich): sir, hujjatlar, kundalik
- Hikoya: Ortiqovlar oilasi 1987-yil noyabrda yo‘q bo‘lgan. Uyda 14 ta topiladigan dalil: 4 hujjat, 2 surat, 2 audio lenta, 3 devor belgisi, 3 topishmoq qog‘ozi. Haqiqat (oxirgi ochilish) keyingi bosqichlarga qoldirilgan — kundalikda «???» bo‘lib turadi.
- E — dalilni olish va o‘qish. J (yoki 📖 tugmasi) — kundalik: Hujjatlar / Suratlar / Audio / Belgilar / Topishmoq / Xronologiya. Topilmagan dalillar qulflangan, qaysi xonada ekani aytiladi.
- Co-op: dalilni host tasdiqlaydi (bir dalilni ikki marta olib bo‘lmaydi), ikkala o‘yinchining kundaligida paydo bo‘ladi; keyin ulangan o‘yinchiga holat yuboriladi.
- Kashfiyotlar faqat joriy o‘yin davomida saqlanadi (sahifa yangilansa uy qayta boshlanadi).
- Zaxira nusxa: BACKUP-v3-step1.zip.

## YANGILANISH 4 (4–5-bosqich): topishmoqlar va yashirin xonalar
Zanjir: **B** ikki tugma (yotoqxona + omborxona, co-opda 7 s, yakka o‘yinda 25 s) → omborxonadagi javon suriladi → **Yashirin ombor** → **C** seyf (kod 1987; kalit + «oxirgi yozuv» qog‘ozi) → **A** belgilar eshigi (Oy → Tog‘ → Suv; kalit kerak) → **Pastki xona** → **D** quvurga 3-2-1 taqillatish → **E** ikki richag (co-opda 3 s, yakka 20 s) → eng chuqur xona (so‘nggi hujjat).
- Hamma holat host tomonidan tekshiriladi va ikkala o‘yinchiga yuboriladi; kech ulangan o‘yinchi to‘liq holatni oladi.
- Xonalar uyning sharqiy devori orqasida (x 20–38). Mos devor/javon topilmasa, bu qism o‘chiriladi va asosiy o‘yin buzilmaydi.
- Zaxira: BACKUP-v4-phase3.zip. Hali yo‘q: tasodifiy voqealar, uy xotirasi, 3 ta yakun (6–8-bosqichlar).
