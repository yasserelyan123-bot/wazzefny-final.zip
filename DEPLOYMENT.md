# وظّفني - تعليمات النشر (نسخة مستقلة)

## نظرة عامة
منصة وظائف متكاملة **"وظّفني"** مبنية بـ **React + Express + PostgreSQL + JWT Authentication**

✅ **مستقلة تماماً** - لا تعتمد على أي خدمة خارجية

---

## المتطلبات الأساسية

- Node.js 18+
- PostgreSQL 12+
- npm أو pnpm

---

## المتغيرات البيئية (بسيطة جداً)

```env
# قاعدة البيانات (مثال PostgreSQL)
DATABASE_URL=postgresql://user:password@host:5432/wazzefni

# المصادقة
JWT_SECRET=your-super-secret-key-change-this-in-production

# البيئة
NODE_ENV=production
```

**ملاحظة:** هذا كل ما تحتاجه! لا توجد متغيرات إضافية.

---

## النشر على Railway

### الخطوة 1: إنشاء مشروع على Railway
```bash
npm install -g railway
railway login
```

### الخطوة 2: تهيئة المشروع
```bash
cd wazzefni-platform
railway init
```

### الخطوة 3: إضافة PostgreSQL
```bash
railway add
# اختر PostgreSQL من القائمة
```

### الخطوة 4: تعيين المتغيرات البيئية
```bash
railway variables set JWT_SECRET="your-secret-key-here"
```

**ملاحظة:** `DATABASE_URL` سيتم ربطه تلقائياً من PostgreSQL

### الخطوة 5: النشر
```bash
railway up
```

سيتم النشر فوراً والحصول على رابط ثابت مثل: `https://wazzefni-production.up.railway.app`

---

## النشر على Render

### الخطوة 1: إنشاء حساب على Render
اذهب إلى https://render.com وأنشئ حساباً

### الخطوة 2: إنشاء PostgreSQL Database
1. اختر "New +" → "PostgreSQL"
2. اختر الخطة المجانية
3. انتظر إنشاء قاعدة البيانات
4. انسخ `Internal Database URL`

### الخطوة 3: إنشاء Web Service
1. اختر "New +" → "Web Service"
2. اربط مع GitHub repo (أو استخدم Render Git)
3. اختر الفرع الرئيسي

### الخطوة 4: إعدادات البناء
- **Name:** wazzefni
- **Build Command:** `npm install && npm run build`
- **Start Command:** `npm start`

### الخطوة 5: متغيرات البيئة
أضف في "Environment":
```
DATABASE_URL=<paste-the-internal-url-from-postgres>
JWT_SECRET=your-secret-key-here
NODE_ENV=production
```

### الخطوة 6: النشر
انقر "Create Web Service" وسيبدأ النشر تلقائياً

سيحصل على رابط مثل: `https://wazzefni.onrender.com`

---

## النشر على Vercel (Frontend فقط)

### الطريقة 1: GitHub Integration
1. ادفع الكود إلى GitHub
2. اذهب إلى https://vercel.com/new
3. اختر GitHub repo
4. اختر `dist/public` كـ Output Directory
5. أضف متغيرات البيئة (إذا لزم الأمر)
6. انقر "Deploy"

### الطريقة 2: Vercel CLI
```bash
npm install -g vercel
vercel --prod
```

---

## البناء والتطوير المحلي

### التثبيت
```bash
npm install
# أو
pnpm install
```

### تشغيل في وضع التطوير
```bash
npm run dev
```

الموقع سيكون متاحاً على: `http://localhost:3000`

### البناء للإنتاج
```bash
npm run build
```

### تشغيل الخادم المُبني
```bash
npm start
```

---

## هيكل المشروع

```
wazzefni-platform/
├── client/                 # React Frontend
│   ├── src/
│   │   ├── pages/         # صفحات التطبيق
│   │   ├── components/    # مكونات React
│   │   └── contexts/      # React Contexts
│   └── index.html
├── server/                # Express Backend
│   ├── routers.ts         # إجراءات tRPC
│   ├── db.ts              # دوال قاعدة البيانات
│   ├── auth.ts            # نظام JWT المصادقة
│   └── _core/             # نظام المصادقة
├── drizzle/               # تعريفات قاعدة البيانات
│   ├── schema.ts          # جداول PostgreSQL
│   └── migrations/        # ملفات الهجرة
├── package.json
├── vite.config.ts
└── tsconfig.json
```

---

## المميزات

✅ **الصفحات:**
- الصفحة الرئيسية مع شريط بحث متقدم
- قائمة الوظائف مع 6 فلاتر
- صفحة تفاصيل الوظيفة
- تسجيل دخول/تسجيل (email + password)
- لوحات تحكم (شركات/مديرين)
- صفحة الأسعار والباقات
- صفحات إضافية (عن، تواصل، سياسة)

✅ **الميزات:**
- نظام متعدد اللغات (عربي/إنجليزي)
- RTL/LTR تلقائي
- 18 وظيفة تجريبية
- 10 شركات حقيقية
- Meta tags و SEO
- Sitemap و robots.txt
- Code splitting محسّن
- Lazy loading للصفحات

---

## استكشاف الأخطاء

### خطأ: "Database connection failed"
```
✅ الحل:
1. تأكد من أن DATABASE_URL صحيح
2. تأكد من أن PostgreSQL قيد التشغيل
3. تأكد من أن كلمة المرور صحيحة
```

### خطأ: "JWT_SECRET is not set"
```
✅ الحل:
1. أضف JWT_SECRET في متغيرات البيئة
2. استخدم قيمة قوية (أكثر من 32 حرف)
```

### الموقع بطيء
```
✅ الحل:
1. تأكد من تشغيل `npm run build` قبل النشر
2. تحقق من حجم الـ bundle (يجب أن يكون < 500KB)
3. استخدم CDN لتسريع الملفات الثابتة
```

---

## أوامر مهمة

```bash
# التثبيت
npm install

# التطوير
npm run dev

# البناء
npm run build

# الإنتاج
npm start

# الاختبارات
npm test

# التحقق من TypeScript
npm run check
```

---

## الأمان

⚠️ **نقاط مهمة:**

1. **غيّر JWT_SECRET** - استخدم قيمة قوية في الإنتاج
2. **استخدم HTTPS** - جميع منصات النشر توفر HTTPS افتراضياً
3. **قاعدة البيانات** - استخدم كلمات مرور قوية
4. **لا تشارك المتغيرات البيئية** - لا تضعها في الكود

---

## الدعم والمساعدة

- [Railway Documentation](https://docs.railway.app)
- [Render Documentation](https://render.com/docs)
- [Vercel Documentation](https://vercel.com/docs)
- [PostgreSQL Documentation](https://www.postgresql.org/docs)

---

## الملفات المهمة

- `package.json` - المكتبات والأوامر
- `drizzle/schema.ts` - تعريف جداول قاعدة البيانات
- `server/auth.ts` - نظام JWT المصادقة
- `server/db.ts` - دوال قاعدة البيانات
- `server/routers.ts` - API endpoints

---

**آخر تحديث:** 21 مايو 2026
**الإصدار:** 2.0 (مستقل تماماً)
