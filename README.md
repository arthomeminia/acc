# نظام إدارة العقارات والاستثمار

نظام ويب متكامل لإدارة شركة استثمار عقاري ومقاولات مكتوب بلغة PHP مع Laravel Framework.

## المميزات الرئيسية

### 🏢 إدارة العقارات
- إدارة المشاريع والبلوكات والوحدات
- تتبع حالة الوحدات (متاح/محجوز/مباع)
- رفع الصور والمستندات للوحدات
- إدارة الأسعار والخصومات

### 👥 إدارة العملاء
- سجل شامل للعملاء مع البيانات الشخصية
- تصنيف العملاء (مشترون/مستثمرون/وسطاء)
- كشف حساب تفصيلي لكل عميل
- إمكانية إرسال كشف الرصيد عبر واتساب

### 💰 المبيعات والعقود
- نظام حجز أولي ثم تحويل لعقد نهائي
- دعم البيع نقداً أو بالتقسيط
- توليد تلقائي لجداول الأقساط
- قوالب عقود قابلة للتخصيص مع تصدير PDF

### 💳 المدفوعات والأقساط
- تسجيل جميع أنواع المدفوعات (نقد، تحويل، شيك، POS)
- تتبع الأقساط المستحقة والمتأخرة
- إشعارات تلقائية للأقساط المستحقة
- إيصالات محاسبية قابلة للطباعة

### 📊 التقارير والإحصائيات
- تقارير مبيعات مفصلة حسب الفترة والمشروع
- تقارير المدفوعات والمصروفات
- كشف حساب العملاء
- تقارير الأقساط المتأخرة
- تصدير التقارير إلى Excel و PDF

### 📱 تكامل واتساب
- إرسال تذكيرات الأقساط المستحقة
- إشعارات تأكيد الدفع
- كشف الرصيد الشهري
- قوالب رسائل قابلة للتخصيص

### 🔐 الأمان والصلاحيات
- نظام صلاحيات متعدد المستويات
- تسجيل جميع العمليات (Audit Log)
- حماية من CSRF, XSS, SQL Injection
- تشفير البيانات الحساسة

## متطلبات النظام

- PHP >= 8.1
- Composer
- SQLite (أو MySQL/PostgreSQL)
- Node.js & NPM (للتطوير)

## التثبيت

### 1. استنساخ المشروع
```bash
git clone <repository-url>
cd sales
```

### 2. تثبيت التبعيات
```bash
composer install
npm install
```

### 3. إعداد البيئة
```bash
cp .env.example .env
php artisan key:generate
```

### 4. إعداد قاعدة البيانات
```bash
php artisan migrate
php artisan db:seed --class=PermissionSeeder
php artisan db:seed --class=UserSeeder
```

### 5. إنشاء رابط التخزين
```bash
php artisan storage:link
```

### 6. تشغيل الخادم
```bash
php artisan serve
```

## الحسابات التجريبية

| الدور | البريد الإلكتروني | كلمة المرور |
|-------|------------------|-------------|
| مدير النظام | admin@example.com | password |
| مدير | manager@example.com | password |
| موظف | employee@example.com | password |
| مشاهد | viewer@example.com | password |

## إعداد واتساب

### 1. إنشاء حساب واتساب بزنس
1. اذهب إلى [WhatsApp Business API](https://business.whatsapp.com/products/business-api)
2. أنشئ حساب جديد
3. احصل على API Key و Phone Number ID

### 2. تحديث ملف .env
```env
WHATSAPP_API_URL=https://graph.facebook.com/v17.0
WHATSAPP_API_KEY=your_api_key_here
WHATSAPP_PHONE_NUMBER_ID=your_phone_number_id_here
WHATSAPP_ACCESS_TOKEN=your_access_token_here
WHATSAPP_WEBHOOK_VERIFY_TOKEN=your_webhook_verify_token_here
```

### 3. إعداد Webhook
- URL: `https://yourdomain.com/whatsapp/webhook`
- Verify Token: نفس القيمة في .env

## هيكل المشروع

```
app/
├── Http/
│   ├── Controllers/     # المتحكمات
│   └── Middleware/      # الوسطاء
├── Models/              # النماذج
└── Services/            # الخدمات

database/
├── migrations/          # ملفات الهجرة
└── seeders/            # ملفات البذور

resources/
├── views/              # القوالب
└── css/               # ملفات CSS

routes/
└── web.php            # مسارات الويب
```

## الأدوار والصلاحيات

### الأدوار
- **مدير النظام**: جميع الصلاحيات
- **مدير**: إدارة المشاريع والعقود والمدفوعات
- **موظف**: إدارة العملاء والوحدات
- **مشاهد**: عرض البيانات فقط

### الصلاحيات
- `dashboard.view`: عرض لوحة التحكم
- `projects.*`: إدارة المشاريع
- `units.*`: إدارة الوحدات
- `customers.*`: إدارة العملاء
- `contracts.*`: إدارة العقود
- `payments.*`: إدارة المدفوعات
- `reports.*`: عرض التقارير
- `whatsapp.*`: إدارة واتساب
- `users.*`: إدارة المستخدمين
- `roles.*`: إدارة الأدوار
- `permissions.*`: إدارة الصلاحيات

## API Endpoints

### الإحصائيات
- `GET /api/stats` - إحصائيات عامة
- `GET /api/sales-chart` - رسم بياني للمبيعات
- `GET /api/projects-chart` - رسم بياني للمشاريع
- `GET /api/customers-chart` - رسم بياني للعملاء

### واتساب
- `POST /whatsapp/send-installment-reminder` - إرسال تذكير بقسط
- `POST /whatsapp/send-payment-confirmation` - تأكيد دفع
- `POST /whatsapp/send-monthly-statement` - كشف رصيد شهري
- `POST /whatsapp/send-custom-message` - رسالة مخصصة
- `POST /whatsapp/send-bulk-message` - رسالة جماعية

## التطوير

### تشغيل في وضع التطوير
```bash
php artisan serve
npm run dev
```

### بناء الأصول
```bash
npm run build
```

### تشغيل الاختبارات
```bash
php artisan test
```

## التخصيص

### الألوان
يمكن تخصيص الألوان من خلال ملف `public/css/app.css`:

```css
:root {
    --primary-color: #2c5aa0;
    --secondary-color: #f8f9fa;
    --accent-color: #28a745;
    /* ... */
}
```

### الخطوط
النظام يستخدم خط Cairo من Google Fonts. يمكن تغييره من خلال ملف `public/css/app.css`.

### القوالب
جميع القوالب موجودة في `resources/views/` ويمكن تخصيصها حسب الحاجة.

## الأمان

### حماية البيانات
- تشفير كلمات المرور
- حماية من SQL Injection
- حماية من XSS
- حماية من CSRF

### تسجيل العمليات
جميع العمليات مسجلة في جدول `audit_logs` مع:
- المستخدم الذي قام بالعملية
- نوع العملية
- البيانات القديمة والجديدة
- الوقت والتاريخ
- عنوان IP

## الدعم

للحصول على الدعم أو الإبلاغ عن مشاكل:
1. تحقق من ملف `storage/logs/laravel.log`
2. تأكد من صحة إعدادات قاعدة البيانات
3. تحقق من صلاحيات الملفات

## الترخيص

هذا المشروع مرخص تحت رخصة MIT.

## المساهمة

نرحب بالمساهمات! يرجى:
1. Fork المشروع
2. إنشاء branch جديد
3. إجراء التغييرات
4. إرسال Pull Request

## التحديثات المستقبلية

- [ ] تطبيق موبايل
- [ ] تكامل مع أنظمة الدفع
- [ ] تقارير متقدمة
- [ ] إشعارات push
- [ ] تكامل مع CRM

---

**تم تطوير هذا النظام بواسطة فريق التطوير**