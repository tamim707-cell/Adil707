# QQE Mod + Ultimate Moving Average Strategy

استراتيجية تداول لمنصة **TradingView** تجمع بين مؤشري **QQE Mod** و **Ultimate Moving Average**، مكتوبة بلغة **Pine Script v6**.

A [TradingView](https://www.tradingview.com/) Pine Script **v6** strategy that combines the **QQE Mod** and **Ultimate Moving Average** indicators.

---

## 📊 المؤشرات المستخدمة / Indicators used

- **QQE Mod** – نفس مؤشر QQE Mod القياسي (نسخة Mihkel00) الموجود على TradingView: هيستوجرام (أعمدة) يتحول للأخضر/الأحمر حول خط الأساس الأبيض (الصفر).
- **Ultimate Moving Average** – نفس مؤشر **`CM_Ultimate_MA_MTF`** (ChrisMoody) الموجود على TradingView: متوسط متحرك بـ 8 أنواع (SMA, EMA, WMA, HullMA, VWMA, RMA, TEMA, Tilson T3) يتحول للأخضر عند الصعود وللأحمر عند الهبوط، مع دعم الإطارات المتعددة (MTF).

> السكربت يعيد بناء **نفس المؤشرَين الأصليَّين** المنشورَين على TradingView داخل ملف واحد، لتطابق الإشارات ما تراه على المنصة.

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

## 📁 الملفات / Files

| الملف | النوع | الوصف |
|-------|------|-------|
| [`qqe_ultimate_ma_strategy.pine`](./qqe_ultimate_ma_strategy.pine) | **Strategy** | ينفّذ صفقات تلقائية مع **وقف خسارة / جني أرباح** ويظهر في **Strategy Tester** |
| [`qqe_ultimate_ma_indicator.pine`](./qqe_ultimate_ma_indicator.pine) | **Indicator** | يعرض إشارات شراء/بيع وتنبيهات فقط **بدون تنفيذ صفقات** |

## ⚙️ طريقة الإضافة / How to install

1. افتح TradingView → **Pine Editor** (المحرّر في أسفل الشاشة).
2. انسخ محتوى الملف الذي تريده (الاستراتيجية أو المؤشر) والصقه.
3. اضغط **Add to chart / إضافة إلى الرسم البياني**.
4. اضبط الإطار الزمني على **1h** وفعّل هايكن آشي إن أردت.
5. (للاستراتيجية) افتح تبويب **Strategy Tester** لمراجعة النتائج التاريخية (Backtest).

## 🎯 وقف الخسارة وجني الأرباح / Stop Loss & Take Profit (في الاستراتيجية)

يدعم السكربت وضعين لحساب الوقف والهدف:

- **ATR** (افتراضي): الوقف = ATR × 2، الهدف = ATR × 4 (قابلة للتعديل).
- **Percent**: الوقف = 2%، الهدف = 4% من سعر الدخول.

بالإضافة إلى ذلك، تُغلق الصفقة تلقائياً عند ظهور إشارة بيع QQE (أيهما أسبق). يمكن تعطيل الوقف/الهدف بالكامل من خيار `Enable Stop Loss / Take Profit`.

### 🔻 الوقف المتحرك / Trailing Stop

فعّل `Enable Trailing Stop` لتفعيل وقف متحرك يتبع السعر:
- `Trail activation = ATR x` — مقدار الربح (بمضاعفات ATR) قبل أن يبدأ الوقف المتحرك بالعمل.
- `Trail distance = ATR x` — المسافة التي يتبع بها الوقف السعر (بمضاعفات ATR).

يمكن استخدام الوقف الثابت والمتحرك معاً؛ يُنفَّذ أيهما يُلمَس أولاً.

## 🔔 التنبيهات و Webhook للتداول الآلي / Alerts & Webhook

كلا الملفين يوفّران تنبيهات جاهزة للربط مع **Webhook** (بوتات التداول الآلي) بصيغة **JSON**:

```json
{"action":"buy","symbol":"{{ticker}}","price":"{{close}}"}
{"action":"sell","symbol":"{{ticker}}","price":"{{close}}"}
```

- **في المؤشر**: اختر شرط التنبيه `Buy Webhook (JSON)` أو `Sell Webhook (JSON)` عند إنشاء تنبيه، أو استخدم تنبيه `alert()` التلقائي عند إغلاق الشمعة.
- **في الاستراتيجية**: عدّل نص رسالة JSON من مجموعة `Alerts / Webhook`، ثم أنشئ تنبيهاً من نوع **"Order fills and alert() function calls"** لإرسال الرسالة إلى الـ Webhook تلقائياً عند تنفيذ الصفقات.

خطوات إنشاء التنبيه: زر **Alert (⏰)** → اختر المؤشر/الاستراتيجية كـ Condition → ضع رابط الـ Webhook في تبويب **Notifications → Webhook URL**.

---

## 🔧 الإعدادات / Inputs

| Input | Default | الوصف |
|-------|---------|-------|
| Use Heikin Ashi source | on | حساب الإشارات على شموع هايكن آشي |
| Restrict entries to 1H | off | السماح بالدخول فقط على إطار الساعة |
| Require general uptrend for Buy | on | اشتراط اتجاه صاعد عام قبل الشراء |
| Uptrend EMA length | 200 | طول المتوسط المستخدم لفلتر الاتجاه |
| QQE Mod parameters | Mihkel00 defaults | إعدادات مؤشر QQE Mod القياسية |
| Ultimate MA Length | 20 | طول المتوسط المتحرك النهائي |
| Ultimate MA Type | 1 (SMA) | نوع المتوسط: 1=SMA 2=EMA 3=WMA 4=HullMA 5=VWMA 6=RMA 7=TEMA 8=T3 |
| Color Smoothing | 2 | عدد الشموع لتحديد اتجاه اللون (1 = بدون تنعيم) |

---

## 🔔 التنبيهات / Alerts

يوفّر السكربت شرطي تنبيه جاهزين (`Buy Signal` و `Sell Signal`) يمكن ربطهما بأي تنبيه في TradingView.

---

## ⚠️ إخلاء مسؤولية / Disclaimer

هذا السكربت لأغراض تعليمية فقط وليس نصيحة مالية. التداول ينطوي على مخاطر؛ اختبر الاستراتيجية جيداً قبل استخدام أموال حقيقية.

*This script is for educational purposes only and is not financial advice. Trading involves risk — backtest thoroughly before risking real capital.*
