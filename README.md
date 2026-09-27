# Daily — Habit Journal (نسخة جاهزة للهاتف / PWA)

هذا المجلد يحتوي على تطبيقك جاهزًا كـ **PWA** (تطبيق ويب تقدّمي):
يعمل بدون إنترنت، له أيقونة، ويمكن تحويله إلى **APK أندرويد حقيقي** بخطوات بسيطة بدون كتابة كود.

## محتويات المجلد
```
index.html        ← التطبيق نفسه (مع كل تحسيناتك)
manifest.json      ← بيانات التطبيق (الاسم، الأيقونة، الألوان)
sw.js               ← يجعل التطبيق يعمل أوفلاين
icons/              ← أيقونات التطبيق (192px, 512px, maskable)
```

البيانات (العادات، اليوميات، الملاحظات) تُحفظ محليًا على جهاز المستخدم (localStorage)،
وتبقى محفوظة حتى بدون إنترنت، وحتى بعد تحويله لتطبيق أندرويد.

---

## الخطوة 1: رفع الملفات على GitHub

1. أنشئ حسابًا على [github.com](https://github.com) إن لم يكن لديك واحد.
2. اضغط **New repository** وأعطه اسمًا مثل `daily-habit-app` واجعله **Public**.
3. ارفع كل الملفات الموجودة في هذا المجلد (بنفس البنية: `index.html`, `manifest.json`, `sw.js`, ومجلد `icons`) — إمّا بالسحب والإفلات من صفحة الريبو مباشرة (Add file → Upload files)، أو عبر Git من جهازك.
4. بعد الرفع، اذهب إلى **Settings → Pages**.
5. تحت "Build and deployment" اختر **Deploy from a branch**، ثم الفرع `main` والمجلد `/ (root)`، واضغط **Save**.
6. انتظر دقيقة أو اثنتين، سيظهر لك رابط مثل:
   ```
   https://USERNAME.github.io/daily-habit-app/
   ```
   افتحه للتأكد أن التطبيق يعمل بشكل صحيح.

---

## الخطوة 2: تحويله إلى APK أندرويد

### الطريقة الموصى بها (مجانية، رسمية، بدون كود) — PWABuilder
1. اذهب إلى [www.pwabuilder.com](https://www.pwabuilder.com)
2. الصق رابط GitHub Pages الذي حصلت عليه، واضغط **Start**.
3. سيفحص الموقع تطبيقك (سيجد الـ manifest والـ service worker جاهزين تلقائيًا).
4. اضغط **Package for stores** ثم اختر **Android**.
5. اترك الإعدادات الافتراضية (أو غيّر اسم الحزمة Package ID إن أردت)، ثم اضغط **Generate**.
6. سيُنزَّل لك ملف مضغوط يحتوي مشروع أندرويد (Trusted Web Activity) جاهز.
7. لتحويله إلى APK فعلي تحتاج أحد الخيارين:
   - **الأسهل:** ثبّت [Android Studio](https://developer.android.com/studio) وافتح المشروع المُنزَّل، ثم من القائمة `Build → Build Bundle(s) / APK(s) → Build APK(s)`.
   - **بدون Android Studio:** ثبّت أداة [Bubblewrap CLI](https://github.com/GoogleChromeLabs/bubblewrap) (تحتاج Node.js + Java JDK فقط)، ثم نفّذ:
     ```
     npm i -g @bubblewrap/cli
     bubblewrap init --manifest=https://USERNAME.github.io/daily-habit-app/manifest.json
     bubblewrap build
     ```
     سينتج لك ملف `app-release-signed.apk` جاهز للتثبيت مباشرة.

### الطريقة الأسرع (تجريبية / بدون Android Studio)
مواقع تحوّل أي رابط ويب إلى APK مباشرة (تكفي رابط GitHub Pages من الخطوة 1):
- [websitetoapk.com](https://websitetoapk.com)
- [appsgeyser.com](https://appsgeyser.com)
- [median.co](https://median.co) (فيه خطة مدفوعة لكن مناسب لتطبيقات احترافية)

فقط ضع رابط GitHub Pages، اختر اسم وأيقونة التطبيق، واضغط توليد — ستحصل على APK جاهز للتنزيل والتثبيت مباشرة على هاتفك.

---

## ملاحظات
- التطبيق يحفظ البيانات محليًا في الهاتف، فإن حذفت التطبيق أو مسحت بياناته تُفقد البيانات (يوجد زر تصدير/استيراد JSON داخل صفحة Setup للنسخ الاحتياطي).
- لتثبيت APK على أندرويد يجب تفعيل "تثبيت من مصادر غير معروفة" (Install unknown apps) من إعدادات الهاتف.
- إن أردت لاحقًا نشره على متجر Google Play، فخيار PWABuilder + Bubblewrap هو الأنسب لأنه ينتج ملف AAB متوافق مع المتجر.
