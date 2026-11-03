# عقل فِكرتك — إعداد Backend آمن

## ما الذي يفعله؟
- واجهة محادثة داخل الموقع.
- Cloudflare Worker وسيط يتصل بـ OpenAI Responses API.
- مفتاح OpenAI يبقى Secret داخل إعدادات Worker ولا يظهر في المتصفح أو GitHub.
- لا يخزن Worker المحادثة؛ الواجهة تحتفظ بسياق محدود داخل ذاكرة الصفحة فقط.

## النشر من الهاتف
1. أنشئ حسابًا في Cloudflare وافتح Workers & Pages.
2. أنشئ Worker باسم fikratak-ai.
3. انسخ محتوى `worker.js` إلى محرر Worker ثم Deploy.
4. من Settings → Variables and Secrets أضف:
   - Secret: `OPENAI_API_KEY` = مفتاح API الخاص بك.
   - Variable: `ALLOWED_ORIGIN` = `https://ag8991852-ship-it.github.io`
   - اختياري Variable: `OPENAI_MODEL` = اسم نموذج متاح لحساب API لديك.
5. انسخ رابط Worker المنشور، ثم في `index.html` استبدل:
   `https://YOUR-WORKER-NAME.YOUR-SUBDOMAIN.workers.dev/chat`
   بالرابط الحقيقي متبوعًا بـ `/chat`.
6. اختبر إرسال رسالة من الموقع.

## الأمان والتكاليف
- لا تضع مفتاح API في `index.html` أو أي ملف داخل المستودع.
- استخدم مفتاحًا مخصصًا للمشروع مع حدود إنفاق ومراقبة الاستخدام من لوحة OpenAI.
- قبل فتح الخدمة للجمهور، أضف حماية إساءة الاستخدام/حدود طلبات على مستوى Cloudflare (Rate Limiting أو Turnstile).
- لا يوجد في هذه النسخة تعلم تلقائي من بيانات المستخدمين. أي تحسين جماعي لاحق يجب أن يعتمد على موافقة واضحة وبيانات مجمعة غير معرّفة.
