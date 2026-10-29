# مدرسة التراث الكربلائي الحسيني

موقع المدرسة (صفحات ثابتة على GitHub Pages + قاعدة بيانات Supabase).

## الملفات

- `index.html` — الموقع
- `notifications.js` — جرس الإشعارات داخل الموقع (صوت + اهتزاز)
- `service-worker.js` — استقبال إشعارات الهاتف حتى والموقع مغلق
- `manifest.json` والأيقونات — لتثبيت الموقع كتطبيق
- `supabase/functions/push/index.ts` — دالة إرسال الإشعارات (Edge Function)

## تفعيل إشعارات الهاتف (مرة واحدة)

1. في Supabase: Edge Functions ← Secrets، أضف:
   - `VAPID_PUBLIC_KEY`
   - `VAPID_PRIVATE_KEY`
   - `VAPID_SUBJECT` (مثال: `mailto:you@example.com`)

   المفتاح العام نفسه يجب أن يكون في `index.html` في المتغير `VAPID_PUBLIC_KEY`.
2. انشر الدالة (مع إيقاف Verify JWT):

   ```sh
   supabase functions deploy push --no-verify-jwt
   ```
3. يفتح الطالب الموقع ويضغط «🔔 تفعيل التنبيهات» مرة واحدة.

ملاحظة: الدالة تستخدم الجدول الموجود `push_subscriptions` (الأعمدة: `user_id`, `endpoint`, `p256dh`, `auth`).
