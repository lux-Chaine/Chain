# Chain-Luxe Hotel Management System

<div align="center">

<img src="Data Analysis/logo.png" alt="Chain-Luxe Logo" width="150" height="150">

![Chain-Luxe Logo](https://img.shields.io/badge/Chain--Luxe-Hotel%20Management%20System-blue)
![Version](https://img.shields.io/badge/version-2.0.0-green)
![Status](https://img.shields.io/badge/status-Tech%20Stack%20Selected-success)
![Svelte](https://img.shields.io/badge/Frontend-Svelte-orange)
![.NET](https://img.shields.io/badge/Backend-.NET%20Core-purple)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blue)

**نظام إدارة فنادق متعدد المستأجرين (Multi-Tenant)**

[English](#english) | [العربية](#arabic)

</div>

---

## 🏨 نبذة عن المشروع

مشروع **Chain-Luxe** هو نظام إدارة فنادق متكامل وحديث مصمم لإدارة مجموعة من الفنادق المتعددة من مقر رئيسي واحد (Head Office). النظام مبني على معمارية Multi-Tenant للسماح بإدارة عدة فنادق مع الحفاظ على عزل البيانات والمرونة في التخصيص.

### الفنادق التابعة لـ Chain-Luxe

1. **فندق أمون** - الإسكندرية
2. **فندق بالم** - كفر الشيخ
3. **فندق الوادي الجديد** - سيوة

---

## 📊 محتويات المشروع

هذا المستودع يحتوي على تحليل شامل وتصميم قاعدة البيانات لنظام Chain-Luxe Hotel Management System.

### الملفات الموجودة

| الملف | الوصف |
|-------|-------|
| `Data Analysis/V8.dbml` | ملف تصميم قاعدة البيانات بتنسيق DBML (142 جدول - معدل لـ Multi-Tenant + جداول الموظفين) |
| `Data Analysis/V8.dbdiagram` | ملف DBDiagram لتصور قاعدة البيانات |
| `Data Analysis/Chain-Luxe_System_Analysis.md` | تحليل شامل للنظام والمعمارية المقترحة |
| `Data Analysis/Chain-Luxe_Implementation_Plan.md` | خطة تنفيذ تفصيلية عامة للمشروع |
| `Data Analysis/Chain-Luxe_Tech_Stack_Plan.md` | خطة تنفيذ مفصلة للتقنيات المختارة (Svelte + .NET + PostgreSQL) |
| `Data Analysis/469 جدول من قاعدة البيانات.txt` | قائمة بأسماء الجداول من النظام القديم |

---

## 🏗️ معمارية النظام

### Multi-Tenant Architecture

النظام مبني على نمط **Shared Database - Shared Schema** حيث:
- جميع الفنادق تشترك في نفس قاعدة البيانات
- جميع الفنادق تشترك في نفس الجداول
- تمييز البيانات يتم عبر عمود `Hotel_Id`
- عزل البيانات يتم عبر Row-Level Security (RLS)

### المميزات

- ✅ كفاءة عالية في استخدام الموارد
- ✅ سهولة الصيانة والتحديث
- ✅ تكلفة أقل للبنية التحتية
- ✅ سهولة عمل تقارير مجمعة للإدارة المركزية

---

## 🗄️ قاعدة البيانات

### الإحصائيات

- **عدد الجداول الأصلية**: 112 جدول
- **عدد الجداول الجديدة المضافة**: 30 جدول (15 Multi-Tenant + 15 إدارة موظفين)
- **إجمالي عدد الجداول**: 142 جدول
- **نوع قاعدة البيانات الأصلية**: Oracle
- **التصميم الحالي**: Multi-Tenant (تم التعديل)

### تصنيف الجداول

1. **جداول إدارة العملاء والملفات الشخصية** (20 جدول)
2. **جداول الحسابات المالية والفواتير** (15 جدول)
3. **جداول الحجوزات والغرف** (25 جدول)
4. **جداول الأسعار والعروض** (12 جدول)
5. **جداول نقاط البيع والمطاعم** (8 جدول)
6. **جداول الأصناف والخدمات** (5 جدول)
7. **جداول الإدارات والضرائب** (7 جدول)
8. **جداول الحركات المالية** (6 جدول)
9. **جداول العملات** (1 جدول)
10. **جداول الإحصائيات والشركاء** (4 جدول)
11. **جداول المفقودات والمعثورات** (1 جدول)
12. **جداول المستخدمين والأنشطة** (1 جدول)
13. **جداول الأنظمة المالية** (1 جدول)
14. **جداول مساعدة** (5 جدول)

---

## 🔧 الجداول الجديدة

تم إضافة **30 جدول جديد** لتحويل النظام إلى Multi-Tenant وإدارة الموظفين:

### جداول Multi-Tenant الأساسية (15 جدول):
1. **Hotels** - جدول الفنادق
2. **Users** - جدول المستخدمين
3. **Roles** - جدول الأدوار
4. **Permissions** - جدول الصلاحيات
5. **RolePermissions** - جدول صلاحيات الأدوار
6. **UserHotelAccess** - جدول روابط المستخدمين بالفنادق
7. **HotelSettings** - جدول إعدادات الفنادق
8. **HotelRoomTypes** - جدول أنواع الغرف لكل فندق
9. **HotelSections** - جدول الوحدات الفرعية
10. **AuditLogs** - جدول سجلات التدقيق
11. **Notifications** - جدول الإشعارات
12. **ScheduledReports** - جدول التقارير المجدولة
13. **SystemIntegrations** - جدول تكامل الأنظمة
14. **Subscriptions** - جدول الاشتراكات والتراخيص
15. **BackupLogs** - جدول النسخ الاحتياطي

### جداول إدارة الموظفين (15 جدول):
16. **Employees** - جدول الموظفين
17. **JobTitles** - جدول المسميات الوظيفية
18. **EmployeeDepartments** - جدول تعيين الموظفين للأقسام
19. **EmployeeShifts** - جدول الورديات
20. **EmployeeAttendance** - جدول الحضور والانصراف
21. **EmployeeLeaves** - جدول الإجازات
22. **EmployeeLeaveBalance** - جدول رصيد الإجازات
23. **EmployeePerformance** - جدول الأداء
24. **EmployeePromotions** - جدول الترقيات
25. **EmployeeTraining** - جدول التدريب

---

## ✅ حالة التنفيذ

### المرحلة الحالية: تصميم قاعدة البيانات ✅

تم إكمال المرحلة الأولى من خطة التنفيذ بنجاح:

#### ✅ المهام المنجزة:
1. **إضافة عمود Hotel_Id** لـ 27 جدول من الجداول الحرجة
2. **إنشاء 15 جدول جديد** لإدارة Multi-Tenant
3. **إنشاء 15 جدول جديد** لإدارة الموظفين (Employees, JobTitles, Shifts, Leaves, etc.)
4. **إنشاء العلاقات (Foreign Keys)** بين الجداول الجديدة
5. **إنشاء العلاقات** بين الجداول المعدلة وجدول Hotels

#### 📊 الإحصائيات:
- **الجداول المعدلة**: 27 جدول
- **الجداول الجديدة**: 30 جدول (15 Multi-Tenant + 15 Employees)
- **العلاقات المضافة**: 60+ علاقة
- **حالة الملف V8.dbml**: ✅ جاهز للتنفيذ

#### 🎯 الخطوات التالية:
1. إنشاء SQL Scripts لتنفيذ التعديلات
2. إنشاء البيانات الأولية للفنادق الثلاثة
3. بدء تطوير الواجهة الخلفية

---

## 🔗 التعديلات المنفذة

### إضافة عمود Hotel_Id

تم إضافة عمود `Hotel_Id` لـ **27 جدول** لتمييز البيانات حسب الفندق:

**جداول العملاء:**
- ✅ Customers
- ✅ CustomerAddresses
- ✅ CustomerCommunications
- ✅ CustomerNotes

**جداول الحسابات:**
- ✅ Accounts
- ✅ FinancialAccounts
- ✅ InvoiceHeaders
- ✅ InvoiceRecords
- ✅ InvoiceDetails
- ✅ Invoices
- ✅ BillingInstructions
- ✅ BillingInstructionHeaders
- ✅ BillingWindows

**جداول الحجوزات:**
- ✅ ReservationsMaster
- ✅ ReservationDetails
- ✅ ReservationPromotions
- ✅ ReservationPosPostings
- ✅ ReservationBoardOptions

**جداول الغرف:**
- ✅ Rooms
- ✅ RoomStatusHistories

**جداول الأسعار:**
- ✅ RateCodeHeaders
- ✅ RateCodeDetails
- ✅ Promotions

**جداول نقاط البيع:**
- ✅ Outlets
- ✅ PosTerminals
- ✅ Tables
- ✅ MenuArticles
- ✅ MenuLinks

**جداول الحركات المالية:**
- ✅ FinancialPostings
- ✅ Cashiers
- ✅ CashierStartingAmounts

**جداول الإدارات:**
- ✅ DepartmentCodes
- ✅ HotelDepartments

**جداول أخرى:**
- ✅ LostAndFound
- ✅ UserActivities
- ✅ FiscalPrinterTransactions
- ✅ SystemParameters

### الجداول المشتركة

هذه الجداول يمكن أن تكون مشتركة بين جميع الفنادق (لا تحتاج Hotel_Id):
- Countries, States, Regions, Cities, Currencies
- AddressTypes, CommunicationTypes, RoomCategories, PaymentTypes, TaxDescriptions

---

## 📚 الوثائق

### التحليل الشامل

ملف `Chain-Luxe_System_Analysis.md` يحتوي على:
- نبذة تفصيلية عن المشروع
- تحليل قاعدة البيانات الحالية
- تحليل معمارية Multi-Tenant
- الجداول الناقصة المقترحة
- التعديلات المطلوبة على الجداول الحالية
- التحديات والمخاطر
- التوصيات النهائية

### خطة التنفيذ

ملف `Chain-Luxe_Implementation_Plan.md` يحتوي على:
- خطة تنفيذ تفصيلية عامة (8 مراحل)
- المهام والمسؤوليات لكل مرحلة
- الفريق المطلوب (9-11 شخص)
- الميزانية التقديرية ($190,000)
- مخاطر المشروع وتخفيفها
- معايير النجاح
- خطة الصيانة بعد الإطلاق

### خطة التقنيات المختارة

ملف `Chain-Luxe_Tech_Stack_Plan.md` يحتوي على:
- خطة تنفيذ تفصيلية للتقنيات المختارة (10 مراحل)
- SvelteKit + Tailwind CSS للواجهة الأمامية
- ASP.NET Core 8 للواجهة الخلفية
- PostgreSQL 15 لقاعدة البيانات
- Entity Framework Core 8 للـ ORM
- Redis للتخزين المؤقت
- JWT + ASP.NET Identity للمصادقة
- WebSocket للتحديثات الحية
- الفريق المطلوب (10 شخص)
- الميزانية التقديرية ($137,400)
- أمثلة على الكود لكل طبقة

---

## 🎯 التقنيات المختارة

### البنية التقنية النهائية

- **Frontend**: SvelteKit + Tailwind CSS
- **Backend**: ASP.NET Core 8
- **Database**: PostgreSQL 15
- **ORM**: Entity Framework Core 8
- **Caching**: Redis
- **Authentication**: JWT + ASP.NET Identity
- **API**: RESTful API + WebSocket (SignalR)

### سبب اختيار هذه التقنيات

#### 🎨 SvelteKit + Tailwind CSS
- **أداء عالي جداً**: Svelte تترجم الكود إلى JavaScript خالص عند البناء
- **حجم صغير**: Bundles أصغر بكثير من React/Vue
- **تصميم سريع**: Tailwind CSS بدون كتابة CSS مخصص
- **مناسب للفنادق**: سريعة الاستجابة لشاشات الاستقبال ونقاط البيع

#### ⚙️ ASP.NET Core 8
- **أداء ممتاز**: أسرع من Node.js للعمليات المعقدة
- **Strong Typing**: C# مع TypeScript يجعل النظام أكثر استقراراً
- **Entity Framework Core**: ORM قوي جداً لقواعد البيانات
- **Enterprise-ready**: مثبت في الشركات الكبرى
- **مناسب للفنادق**: معالجة المعاملات المهمة للحجوزات والفواتير

#### 🗄️ PostgreSQL 15
- **مجاني ومفتوح المصدر**: لا توجد تكاليف ترخيص
- **Row-Level Security (RLS)**: ميزة مدمجة لعزل البيانات (مهمة جداً لـ Multi-Tenant)
- **JSON Support**: دعم ممتاز للبيانات المرنة
- **مناسب للفنادق**: RLS مثالي لعزل بيانات الفنادق

### الأمان

- تشفير كلمات المرور (bcrypt/argon2)
- HTTPS لجميع الاتصالات
- Row-Level Security في قاعدة البيانات
- Audit Log لجميع العمليات الحساسة

### المراقبة

- نظام مراقبة الأداء (Prometheus/Grafana)
- نظام تسجيل الأخطاء (Sentry/ELK)
- تنبيهات فورية للمشاكل

---

## ⚠️ التحديات والمخاطر

### 1. عزل البيانات
- **المخطر**: تسرب البيانات بين الفنادق
- **الحل**: استخدام Row-Level Security (RLS) في قاعدة البيانات

### 2. الأداء
- **المخطر**: بطء الاستعلامات مع كثرة البيانات
- **الحل**: Indexing مخصص على Hotel_Id، Partitioning

### 3. التخصيص
- **المخطر**: كل فندق له متطلبات مختلفة
- **الحل**: نظام إعدادات مرن (HotelSettings)

### 4. المزامنة
- **المخطر**: عدم توازن البيانات بين الفنادق
- **الحل**: نظام مزامنة آلي ومراقبة مستمرة

### 5. النسخ الاحتياطي
- **المخطر**: فقدان بيانات فندق محدد
- **الحل**: نسخ احتياطي على مستوى الفندق باستخدام Hotel_Id

---

## 📈 ملخص المشروع

### النقاط الرئيسية

- ✅ يمكن بناء نظام Multi-Tenant بناءً على قاعدة البيانات الحالية
- ✅ تم إضافة 15 جدول جديد لإدارة الفنادق والمستخدمين والصلاحيات
- ✅ تم تعديل 27 جدول لإضافة Hotel_Id
- ✅ النمط الموصى به: Shared Database - Shared Schema
- ✅ تصميم قاعدة البيانات جاهز للتنفيذ

### الخلاصة

النظام المقترح سيوفر لـ Chain-Luxe منصة موحدة وفعالة لإدارة جميع فنادقها مع الحفاظ على عزل البيانات والمرونة في التخصيص.

---

## 🚀 الخطوات التالية

1. ✅ **تصميم قاعدة البيانات**: مكتمل
2. ✅ **اختيار التقنيات**: مكتمل (Svelte + .NET + PostgreSQL)
3. ⏳ **إنشاء المشاريع**: يجب البدء
4. ⏳ **إعداد البيئة المحلية**: يجب البدء
5. ⏳ **بدء تطوير Backend**: يجب البدء

---

## 📞 التواصل

للاستفسارات والأسئلة، يرجى التواصل مع فريق تطوير Chain-Luxe.

---

## 📝 معلومات المشروع

- **تاريخ البدء**: 14 سبتمبر 2026
- **تاريخ آخر تحديث**: 14 سبتمبر 2026
- **الحالة الحالية**: اختيار التقنيات وإنشاء خطة التنفيذ المفصلة
- **الإصدار**: 2.0.0
- **التقنيات المختارة**: SvelteKit + .NET Core + PostgreSQL
- **المطور**: فريق تطوير Chain-Luxe

---

## 📄 الترخيص

هذا المشروع مملوك لشركة Chain-Luxe. جميع الحقوق محفوظة © 2026

---

<div align="center">

**صُنع بـ ❤️ لفريق Chain-Luxe**

</div>
