# QQE Mod + Ultimate Moving Average Strategy

استراتيجية تداول لمنصة **TradingView** تجمع بين مؤشري **QQE Mod** و **Ultimate Moving Average**، مكتوبة بلغة **Pine Script v6**.

A [TradingView](https://www.tradingview.com/) Pine Script **v6** strategy that combines the **QQE Mod** and **Ultimate Moving Average** indicators.

---

## 📊 المؤشرات المستخدمة / Indicators used

- **QQE Mod** – نسخة مطوّرة من مؤشر QQE تعرض هيستوجرام (أعمدة) يتحول للأخضر/الأحمر حول خط الأساس الأبيض (الصفر).
- **Ultimate Moving Average** – متوسط متحرك متكيّف يتحول للأخضر عند الصعود وللأحمر عند الهبوط.

Both indicators are re-implemented **inside a single script**, so you only need to add one item to your chart.

---

## 🟢 شروط الشراء / Buy rules

1. أن يكون السعر مرتداً من دعم قوي أو في اتجاه صاعد عام *(General uptrend filter)*.
2. تحوّل هيستوجرام **QQE Mod** إلى **الأخضر** مع الإغلاق **فوق** خط الأساس الأبيض (الصفر).
3. تحوّل مؤشر **Ultimate Moving Average** إلى **الأخضر** (صاعد).
4. عند تحقّق كل الشروط → **دخول صفقة شراء**.

The script opens a long only when **all** of these are true on the same bar.

## 🔴 شرط البيع / Sell rule

- إغلاق الصفقة بمجرد أن يتحول **QQE Mod** إلى **الأحمر** ويغلق **تحت** الخط الأبيض.

---

## 💡 سر تعزيز الأرباح / Profit Booster

- **Heikin Ashi**: فعّل الخيار `Use Heikin Ashi source` (مُفعّل افتراضياً) لحساب الإشارات على شموع هايكن آشي.
- **الإطار الزمني**: استخدم إطار **ساعة واحدة (1h)** حصراً. يمكنك تفعيل `Restrict entries to 1H timeframe only` لمنع الدخول على أي إطار آخر.

---

## ⚙️ طريقة الإضافة / How to install

1. افتح TradingView → **Pine Editor** (المحرّر في أسفل الشاشة).
2. انسخ محتوى الملف [`qqe_ultimate_ma_strategy.pine`](./qqe_ultimate_ma_strategy.pine) والصقه.
3. اضغط **Add to chart / إضافة إلى الرسم البياني**.
4. اضبط الإطار الزمني على **1h** وفعّل هايكن آشي إن أردت.
5. (اختياري) افتح تبويب **Strategy Tester** لمراجعة النتائج التاريخية (Backtest).

---

## 🔧 الإعدادات / Inputs

| Input | Default | الوصف |
|-------|---------|-------|
| Use Heikin Ashi source | on | حساب الإشارات على شموع هايكن آشي |
| Restrict entries to 1H | off | السماح بالدخول فقط على إطار الساعة |
| Require general uptrend for Buy | on | اشتراط اتجاه صاعد عام قبل الشراء |
| Uptrend EMA length | 200 | طول المتوسط المستخدم لفلتر الاتجاه |
| QQE Mod parameters | Mihkel00 defaults | إعدادات مؤشر QQE Mod القياسية |
| Ultimate MA Length / Type | 20 / HMA | طول ونوع المتوسط المتحرك النهائي |

---

## 🔔 التنبيهات / Alerts

يوفّر السكربت شرطي تنبيه جاهزين (`Buy Signal` و `Sell Signal`) يمكن ربطهما بأي تنبيه في TradingView.

---

## ⚠️ إخلاء مسؤولية / Disclaimer

هذا السكربت لأغراض تعليمية فقط وليس نصيحة مالية. التداول ينطوي على مخاطر؛ اختبر الاستراتيجية جيداً قبل استخدام أموال حقيقية.

*This script is for educational purposes only and is not financial advice. Trading involves risk — backtest thoroughly before risking real capital.*
