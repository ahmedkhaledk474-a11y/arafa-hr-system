# 🌐 دليل رفع نظام موارد بشرية ورواتب مجموعة عرفه على الإنترنت (مجاناً)

## ✅ الطريقة الموصى بها: Vercel + Neon (PostgreSQL مجاني)

### لماذا هذه الطريقة؟
- **مجاني 100%** للنطاق الشخصي والبداية
- **HTTPS تلقائي** + دومين فرعي (your-app.vercel.app)
- **سرعة عالمية** (CDN)
- **نشر تلقائي** عند كل تحديث للكود
- يدعم آلاف المستخدمين

---

## 📋 الخطوة 1: إنشاء قاعدة بيانات PostgreSQL مجانية على Neon

1. اذهب إلى **https://neon.tech** واضغط **Sign Up** (مجاني)
2. سجّل بحساب GitHub أو Google
3. اضغط **New Project** → اختر اسم (مثل `arafa-hr`)
4. اختر **Region**: الأقرب لك (مثلاً Frankfurt أو Bahrain)
5. اضغط **Create Project**
6. بعد الإنشاء، انسخ **Connection String** (يبدأ بـ `postgresql://...`)
   - احفظه — ستحتاجه في الخطوة 4

---

## 📋 الخطوة 2: رفع الكود على GitHub

1. اذهب إلى **https://github.com** وسجّل دخول
2. اضغط **New repository** → اسمه `arafa-hr-system`
3. اختر **Private** (للخصوصية)
4. اضغط **Create repository**

### رفع الملفات:
```bash
# في مجلد المشروع على جهازك
git init
git add -A
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/arafa-hr-system.git
git push -u origin main
```

أو اسحب ملف الـ zip الذي حمّلته من النظام وفكه ثم ارفعه.

---

## 📋 الخطوة 3: ربط المشروع بـ Vercel

1. اذهب إلى **https://vercel.com** واضغط **Sign Up** (مجاني)
2. سجّل بـ **نفس حساب GitHub**
3. اضغط **Add New Project**
4. اختر مستودع `arafa-hr-system` من القائمة
5. **Framework Preset**: Next.js (سيُكتشف تلقائياً)
6. **Root Directory**: `./` (افتراضي)

---

## 📋 الخطوة 4: إعداد متغيرات البيئة

في صفحة إعداد المشروع على Vercel، اضغط **Environment Variables** وأضف:

| المتغير | القيمة |
|---|---|
| `DATABASE_URL` | Connection String من Neon (الخطوة 1) |
| `JWT_SECRET` | أي نص عشوائي طويل (مثل `arafa-secret-2026-xyz123abc`) |

ثم اضغط **Deploy** ✅

---

## 📋 الخطوة 5: تعديل قاعدة البيانات للعمل مع PostgreSQL

### في ملف `prisma/schema.prisma`، غيّر:
```prisma
datasource db {
  provider = "postgresql"  // كان "sqlite"
  url      = env("DATABASE_URL")
}
```

### ثم شغّل محلياً (قبل الرفع):
```bash
# ثبت Prisma عالمياً (لو غير مثبت)
npm install -g prisma

# أنشئ الجداول في PostgreSQL
prisma db push

# أدخل بيانات تجريبية (لو تريد)
# أو استورد من ملف Excel عبر قسم استيراد البيانات
```

---

## 📋 الخطوة 6: إنشاء حساب الأدمن

بعد النشر، ستحتاج لإنشاء حساب أدمن في قاعدة البيانات الجديدة:

1. اذهب لـ **Neon Console** → **SQL Editor**
2. شغّل هذا الاستعلام (بعد تعديل كلمة المرور):

```sql
-- إنشاء حساب أدمن (كلمة المرور: admin123)
-- ملاحظة: passwordHash مشفّر بـ bcrypt — استخدم الـ API محلياً لإنشائه
INSERT INTO "User" (id, username, passwordHash, role, permissions, loginEnabled, createdAt, updatedAt)
VALUES (
  'admin-001',
  'admin',
  '$2a$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy', -- admin123
  'ADMIN',
  '',
  1,
  datetime('now'),
  datetime('now')
);
```

أو أسهل: شغّل المشروع محلياً مع PostgreSQL، أنشئ الأدمن عبر الـ API، ثم ارفع.

---

## 🎉 الخطوة 7: الوصول للنظام

بعد النشر الناجح، ستحصل على رابط مثل:
```
https://arafa-hr-system.vercel.app
```

- كل الموظفين يمكنهم الدخول من أي مكان
- يعمل على الموبايل والكمبيوتر
- HTTPS آمن

---

## 🔄 التحديثات اللاحقة

عند تعديل الكود:
```bash
git add -A
git commit -m "وصف التعديل"
git push
```
Vercel سينشر التحديث تلقائياً خلال دقيقة ✅

---

## 💡 بديل: VPS مجاني (Render.com)

لو Vercel لا يناسبك:

1. اذهب إلى **https://render.com**
2. أنشئ **Web Service** من مستودع GitHub
3. أضف متغيرات البيئة
4. Render يعطيك رابط مجاني

**المزايا**: يدعم SQLite (لو تريد البقاء عليه)
**العيوب**: النطاق المجاني ينام بعد 15 دقيقة من عدم النشاط

---

## 📞 بيانات الدخول الافتراضية

- **الإدارة**: `admin` / `admin123`
- **الموظف**: `EMP001` / `EMP001`

---

## ❓ مساعدة

لو واجهت أي مشكلة، تواصل مع المطور:
- **أحمد خالد**: 01014230703

---

## 📊 ملخص التكلفة

| الخدمة | التكلفة |
|---|---|
| **GitHub** | مجاني (للحساب الشخصي) |
| **Vercel** | مجاني (Hobby plan) |
| **Neon PostgreSQL** | مجاني (0.5GB — يكفي لآلاف الموظفين) |
| **الدومين** | مجاني (your-app.vercel.app) |
| **الإجمالي** | **0 جنيه** ✅ |
