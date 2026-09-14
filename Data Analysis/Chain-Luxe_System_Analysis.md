# تحليل نظام Chain-Luxe Hotel Management System
## Multi-Tenant Architecture Assessment & Database Design

---

## 📋 نبذة عن المشروع

### الهدف الاستراتيجي
بناء نظام إدارة فنادق متكامل وحديث لشركة **Chain-Luxe** كمنظمة مقرها الرئيسي (Head Office) تدير مجموعة من الفنادق المتعددة.

### السياق والمشكلة
- شركة **Suite 8** (النظام القديم) تم تصميمها لفندق واحد فقط
- النظام القديم مبني على Oracle Database
- قاعدة البيانات الحالية تم استخراجها وتحسينها لتناسب المشروع الجديد
- الهدف: تحويل وبناء أنظمة جديدة تواكب العصر الحالي

### الفنادق التابعة لـ Chain-Luxe
1. **فندق أمون** - الإسكندرية
2. **فندق بالم** - كفر الشيخ
3. **فندق الوادي الجديد** - سيوة

---

## 📊 تحليل قاعدة البيانات الحالية

### الإحصائيات
- **عدد الجداول الحالية**: 112 جدول
- **نوع قاعدة البيانات الأصلية**: Oracle
- **التصميم الحالي**: Single-Tenant (مصمم لفندق واحد)

### تصنيف الجداول الحالية

#### 1. جداول إدارة العملاء والملفات الشخصية (20 جدول)
- `Customers` - العملاء الأساسي
- `CustomerAddresses` - عناوين العملاء
- `CustomerCommunications` - اتصالات العملاء
- `CustomerCategories` - فئات العملاء
- `CustomerCompanyDetails` - تفاصيل الشركات
- `CustomerLinks` - روابط العملاء
- `CustomerNotes` - ملاحظات العملاء
- `CustomerBillingInstructions` - تعليمات الفوترة
- `CorporateContracts` - عقود الشركات
- `CorporateContractCustomerLinks` - ربط العقود بالعملاء
- `AddressTypes` - أنواع العناوين
- `CommunicationTypes` - أنوات الاتصال
- `NotesCategories` - فئات الملاحظات
- `NotesCategoryLinks` - روابط فئات الملاحظات
- `GuestPersonalDocuments` - وثائق الضيوف
- `PersonalDocumentGroups` - مجموعات الوثائق
- `Countries` - الدول
- `States` - الولايات
- `Regions` - المناطق
- `StateZipCodeRanges` - نطاقات الرموز البريدية
- `Cities` - المدن

#### 2. جداول الحسابات المالية والفواتير (15 جدول)
- `Accounts` - حسابات الذمم والقبض
- `AccountTypes` - أنواع حسابات القبض
- `AccountTypeLinks` - روابط أنواع الحسابات
- `FinancialAccounts` - الحسابات المالية الفرعية
- `InvoiceHeaders` - رؤوس الفواتير
- `InvoiceDetails` - تفاصيل الفواتير
- `InvoiceRecords` - سجلات الفواتير
- `InvoicePaymentLinks` - روابط مدفوعات الفواتير
- `Invoices` - الفواتير الرئيسية
- `InvoiceStatuses` - حالات الفواتير
- `BillingInstructions` - تعليمات الفوترة
- `BillingInstructionHeaders` - رؤوس تعليمات الفوترة
- `BillingInstructionDetails` - تفاصيل تعليمات الفوترة
- `BillingWindows` - نوافذ الفوترة
- `BillingWindowTypes` - أنواع نوافذ الفوترة

#### 3. جداول الحجوزات والغرف (25 جدول)
- `ReservationsMaster` - الحجوزات الرئيسية
- `ReservationDetails` - تفاصيل الحجز اليومية
- `ReservationStatuses` - حالات الحجوزات
- `ReservationSources` - مصادر الحجوزات
- `ReservationCriteriaCodes` - معايير الحجوزات
- `ReservationReasonLinks` - روابط أسباب الحجوزات
- `ReservationPromotions` - عروض الحجوزات
- `ReservationPosPostings` - حركات نقاط البيع للحجوزات
- `ReservationBoardOptions` - خيارات الوجبات
- `ReservationDetailLinks` - روابط تفاصيل الحجوزات
- `ReservationDetailData` - بيانات تفاصيل الحجوزات
- `ReservationDetailAgeLines` - خطوط الأعمار
- `ReservationDetailWakeupCalls` - مكالمات الإيقاظ
- `GeneralReservationInformation` - معلومات الحجوزات العامة
- `ReservationRegistrationCardLinks` - روابط بطاقات التسجيل
- `Rooms` - الغرف الرئيسية
- `RoomCategories` - فئات الغرف
- `RoomStatuses` - حالات الغرف
- `RoomStatusReasons` - أسباب حالات الغرف
- `RoomStatusHistories` - تاريخ حالات الغرف
- `RoomAttributeLinks` - روابط خصائص الغرف
- `SuiteRoomCategories` - فئات الأجنحة
- `SuiteRoomLinks` - روابط الأجنحة
- `Barcodes` - الباركود
- `RateCodes` - أكواد الأسعار
- `ReservationCodes` - رموز الحجوزات

#### 4. جداول الأسعار والعروض (12 جدول)
- `RateCodeHeaders` - رؤوس أكواد الأسعار
- `RateCodeDetails` - تفاصيل أكواد الأسعار
- `RateCodeMatrixValues` - قيم مصفوفة الأسعار
- `RateCodeChildMatrixValues` - قيم مصفوفة الأطفال
- `RateCodePackageLinks` - روابط الباقات
- `RateDetailCalendars` - تقويمات الأسعار
- `RateDetailPackageLinks` - روابط تفاصيل الباقات
- `Promotions` - العروض الترويجية
- `BookingBlockSalesDetails` - تفاصيل مبيعات الكتل
- `RebateCardConfig` - تكوين بطاقات الخصم
- `RebateDefinitions` - تعريفات الخصومات
- `RoomResourceCardConfig` - تكوين بطاقات الموارد

#### 5. جداول نقاط البيع والمطاعم (8 جدول)
- `Outlets` - منافذ البيع
- `PosTerminals` - أجهزة نقاط البيع
- `Tables` - الطاولات
- `MenuArticles` - أصناف القائمة
- `MenuLinks` - روابط القوائم
- `MealPeriods` - فترات الوجبات
- `MealPeriodLinks` - روابط فترات الوجبات
- `SystemParameters` - معاملات النظام

#### 6. جداول الأصناف والخدمات (5 جدول)
- `Articles` - الأصناف الرئيسية
- `MenuItems` - عناصر القائمة
- `MenuItemCategories` - فئات عناصر القائمة
- `PaymentTypes` - أنواع وسائل الدفع
- `PaymentAdditions` - إضافات المدفوعات

#### 7. جداول الإدارات والضرائب (7 جدول)
- `DepartmentCodes` - أكواد الأقسام
- `DepartmentTaxesLink` - روابط ضرائب الأقسام
- `DepartmentCurrencyConfig` - تكوين عملات الأقسام
- `InterfaceGroups` - مجموعات الواجهات
- `TaxesConfig` - تكوين الضرائب
- `TaxDescriptions` - أوصاف الضرائب
- `HotelDepartments` - أقسام الفندق

#### 8. جداول الحركات المالية (6 جدول)
- `FinancialPostings` - الحركات المالية الرئيسية
- `PostingInvoiceLink` - روابط الفواتير بالحركات
- `PostingOrigin` - مصدر القيد
- `CustomPostingOriginator` - منشئ القيد المخصص
- `Cashiers` - الصيارفة
- `CashierStartingAmounts` - أرصدة بداية الصيارفة

#### 9. جداول العملات (1 جدول)
- `Currencies` - العملات

#### 10. جداول الإحصائيات والشركاء (4 جدول)
- `StatisticalPartnerRevenue` - إيرادات الشركاء
- `TravelAgentCommissionCodes` - أكواد عمولات وكلاء السفر
- `TravelAgentCommissionRules` - قواعد عمولات وكلاء السفر
- `TravelAgentCommissionLinks` - روابط عمولات وكلاء السفر
- `TravelAgentCommissionDepartmentLinks` - روابط أقسام عمولات وكلاء السفر

#### 11. جداول المفقودات والمعثورات (1 جدول)
- `LostAndFound` - المفقودات والمعثورات

#### 12. جداول المستخدمين والأنشطة (1 جدول)
- `UserActivities` - أنشطة المستخدمين

#### 13. جداول الأنظمة المالية (1 جدول)
- `FiscalPrinterTransactions` - معاملات الطابعة المالية

#### 14. جداول مساعدة (5 جدول)
- `TelephoneBooks` - دليل الهاتف
- `StateZipCodeRanges` - نطاقات الرموز البريدية
- `DaytypeDetailDates` - تفاصيل تواريخ أنواع الأيام
- `CategoryLinks` - روابط الفئات
- `SuiteRoomCategories` - فئات الأجنحة

---

## 🏗️ تحليل إمكانية بناء نظام Multi-Tenant

### ✅ الإجابة: نعم، يمكن بناء نظام Multi-Tenant

بناءً على تحليل قاعدة البيانات الحالية، يمكن تحويل النظام إلى Multi-Tenant Architecture. يوجد عدة أنماط للتنفيذ:

### النمط 1: Shared Database - Shared Schema (الأكثر كفاءة)
**الوصف**: جميع الفنادق تشترك في نفس قاعدة البيانات ونفس الجداول، مع إضافة عمود `Hotel_Id` لتمييز البيانات.

**المميزات**:
- كفاءة عالية في استخدام الموارد
- سهولة الصيانة والتحديث
- تكلفة أقل للبنية التحتية

**العيوب**:
- احتمالية تضارب البيانات (يمكن حلها بـ Row-Level Security)
- صعوبة في النسخ الاحتياطي لفندق محدد

### النمط 2: Shared Database - Separate Schema (متوسط)
**الوصف**: قاعدة بيانات واحدة، لكن لكل فندق Schema خاص به.

**المميزات**:
- عزل البيانات بشكل أفضل
- سهولة في النسخ الاحتياطي لكل فندق

**العيوب**:
- تعقيد أكبر في الإدارة
- استخدام أكبر للموارد

### النمط 3: Separate Database (الأكثر عزلاً)
**الوصف**: لكل فندق قاعدة بيانات منفصلة تماماً.

**المميزات**:
- عزل تام للبيانات
- مرونة كاملة في التخصيص لكل فندق
- سهولة النسخ الاحتياطي والاستعادة

**العيوب**:
- تكلفة عالية للبنية التحتية
- صعوبة في إدارة التحديثات الموحدة

### التوصية: النمط 1 (Shared Database - Shared Schema)
بالنسبة لـ Chain-Luxe مع 3 فنادق فقط، **النمط 1 هو الأنسب** للأسباب التالية:
1. عدد الفنادق صغير (3 فقط)
2. سهولة الإدارة والصيانة
3. كفاءة استخدام الموارد
4. سهولة عمل تقارير مجمعة للإدارة المركزية

---

## 🔧 الجداول الناقصة المقترحة

### الجداول الأساسية المطلوبة لنظام Multi-Tenant

#### 1. جدول الفنادق (Hotels)
```sql
Table Hotels {
  Id bigint [pk]
  Code varchar(10) [unique] -- كود الفندق (مثل: AMON, PALM, SIWA)
  Name varchar(100) -- اسم الفندق بالكامل
  NameArabic varchar(100) -- الاسم بالعربية
  NameEnglish varchar(100) -- الاسم بالإنجليزية
  City varchar(50) -- المدينة
  Country_Id bigint -- الدولة
  Address varchar(200) -- العنوان
  Phone varchar(20) -- الهاتف
  Email varchar(100) -- البريد الإلكتروني
  Website varchar(100) -- الموقع الإلكتروني
  Logo varchar(500) -- رابط الشعار
  TaxNumber varchar(50) -- الرقم الضريبي
  CommercialRegistration varchar(50) -- السجل التجاري
  StarRating int -- عدد النجوم
  RoomCount int -- عدد الغرف
  CheckInTime time -- وقت التسجيل الوصول
  CheckOutTime time -- وقت التسجيل المغادرة
  DefaultCurrency_Id bigint -- العملة الافتراضية
  IsActive int [default: 1] -- حالة التفعيل
  CreatedAt timestamp
  UpdatedAt timestamp
  CreatedBy bigint
  UpdatedBy bigint
}
```

#### 2. جدول المستخدمين (Users)
```sql
Table Users {
  Id bigint [pk]
  Username varchar(50) [unique]
  Email varchar(100) [unique]
  PasswordHash varchar(255)
  FullName varchar(100)
  PhoneNumber varchar(20)
  Hotel_Id bigint -- الفندق الرئيسي للمستخدم
  Role_Id bigint -- الدور
  Department_Id bigint -- القسم
  IsActive int [default: 1]
  LastLogin timestamp
  CreatedAt timestamp
  UpdatedAt timestamp
}
```

#### 3. جدول الأدوار (Roles)
```sql
Table Roles {
  Id bigint [pk]
  Name varchar(50)
  NameArabic varchar(50)
  Description varchar(200)
  IsSystem int [default: 0] -- دور نظامي لا يمكن حذفه
  CreatedAt timestamp
  UpdatedAt timestamp
}
```

#### 4. جدول صلاحيات الأدوار (RolePermissions)
```sql
Table RolePermissions {
  Id bigint [pk]
  Role_Id bigint
  Permission_Id bigint
  CreatedAt timestamp
}
```

#### 5. جدول الصلاحيات (Permissions)
```sql
Table Permissions {
  Id bigint [pk]
  Module varchar(50) -- اسم الوحدة (مثل: Reservations, FrontDesk)
  Action varchar(50) -- الإجراء (مثل: Create, Read, Update, Delete)
  Description varchar(200)
  CreatedAt timestamp
}
```

#### 6. جدول روابط المستخدمين بالفنادق (UserHotelAccess)
```sql
Table UserHotelAccess {
  Id bigint [pk]
  User_Id bigint
  Hotel_Id bigint
  AccessLevel int -- مستوى الوصول (1=Read, 2=Write, 3=Full)
  IsActive int [default: 1]
  CreatedAt timestamp
  UpdatedAt timestamp
}
```

#### 7. جدول إعدادات الفنادق (HotelSettings)
```sql
Table HotelSettings {
  Id bigint [pk]
  Hotel_Id bigint
  SettingKey varchar(100)
  SettingValue text
  Description varchar(200)
  UpdatedAt timestamp
  UpdatedBy bigint
}
```

#### 8. جدول أنواع الغرف لكل فندق (HotelRoomTypes)
```sql
Table HotelRoomTypes {
  Id bigint [pk]
  Hotel_Id bigint
  RoomCategory_Id bigint
  TotalRooms int -- العدد الإجمالي
  AvailableRooms int -- المتاح حالياً
  BasePrice decimal(30,4) -- السعر الأساسي
  IsActive int [default: 1]
  CreatedAt timestamp
  UpdatedAt timestamp
}
```

#### 9. جدول الوحدات الفرعية (HotelBuildings/Sections)
```sql
Table HotelSections {
  Id bigint [pk]
  Hotel_Id bigint
  Name varchar(100)
  NameArabic varchar(100)
  SectionType varchar(50) -- Building, Floor, Wing
  ParentSection_Id bigint -- للهيكل الشجري
  Description varchar(200)
  IsActive int [default: 1]
  CreatedAt timestamp
}
```

#### 10. جدول سجلات التدقيق (AuditLogs)
```sql
Table AuditLogs {
  Id bigint [pk]
  Hotel_Id bigint
  User_Id bigint
  TableName varchar(100)
  RecordId bigint
  ActionType varchar(20) -- INSERT, UPDATE, DELETE
  OldValues json
  NewValues json
  ChangedAt timestamp
  IpAddress varchar(50)
  UserAgent varchar(500)
}
```

#### 11. جدول الإشعارات (Notifications)
```sql
Table Notifications {
  Id bigint [pk]
  Hotel_Id bigint
  User_Id bigint
  Title varchar(200)
  Message text
  Type varchar(50) -- Info, Warning, Error, Success
  IsRead int [default: 0]
  RelatedRecordId bigint
  RelatedTable varchar(100)
  CreatedAt timestamp
}
```

#### 12. جدول التقارير المجدولة (ScheduledReports)
```sql
Table ScheduledReports {
  Id bigint [pk]
  Hotel_Id bigint
  ReportName varchar(100)
  ReportType varchar(50)
  ScheduleType varchar(20) -- Daily, Weekly, Monthly
  Recipients varchar(500) -- قائمة البريد الإلكتروني
  Parameters json
  LastRun timestamp
  NextRun timestamp
  IsActive int [default: 1]
  CreatedBy bigint
  CreatedAt timestamp
}
```

#### 13. جدول تكامل الأنظمة (SystemIntegrations)
```sql
Table SystemIntegrations {
  Id bigint [pk]
  Hotel_Id bigint
  IntegrationType varchar(50) -- POS, PMS, Accounting, CRM
  Provider varchar(100) -- اسم المزود
  ApiEndpoint varchar(500)
  ApiKey varchar(255)
  Configuration json
  IsActive int [default: 1]
  LastSync timestamp
  CreatedAt timestamp
  UpdatedAt timestamp
}
```

#### 14. جدول الاشتراكات والتراخيص (Subscriptions)
```sql
Table Subscriptions {
  Id bigint [pk]
  Hotel_Id bigint
  PlanType varchar(50) -- Basic, Standard, Premium
  StartDate date
  EndDate date
  MaxUsers int
  MaxRooms int
  Features json -- قائمة الميزات المفعلة
  IsActive int [default: 1]
  RenewalDate date
  CreatedAt timestamp
}
```

#### 15. جدول النسخ الاحتياطي (BackupLogs)
```sql
Table BackupLogs {
  Id bigint [pk]
  Hotel_Id bigint
  BackupType varchar(20) -- Full, Incremental
  FilePath varchar(500)
  FileSize bigint
  Status varchar(20) -- Success, Failed, InProgress
  StartedAt timestamp
  CompletedAt timestamp
  CreatedBy bigint
}
```

---

## 🔗 التعديلات المطلوبة على الجداول الحالية

### إضافة عمود Hotel_Id للجداول التالية

#### الجداول التي تحتاج Hotel_Id (43 جدول):

**جداول العملاء:**
- `Customers` - إضافة `Hotel_Id`
- `CustomerAddresses` - إضافة `Hotel_Id`
- `CustomerCommunications` - إضافة `Hotel_Id`
- `CustomerNotes` - إضافة `Hotel_Id`

**جداول الحسابات:**
- `Accounts` - إضافة `Hotel_Id`
- `FinancialAccounts` - إضافة `Hotel_Id`
- `InvoiceHeaders` - إضافة `Hotel_Id`
- `InvoiceDetails` - إضافة `Hotel_Id`
- `InvoiceRecords` - إضافة `Hotel_Id`
- `Invoices` - إضافة `Hotel_Id`
- `BillingInstructionHeaders` - إضافة `Hotel_Id`
- `BillingWindows` - إضافة `Hotel_Id`

**جداول الحجوزات:**
- `ReservationsMaster` - إضافة `Hotel_Id`
- `ReservationDetails` - إضافة `Hotel_Id`
- `ReservationPromotions` - إضافة `Hotel_Id`
- `ReservationPosPostings` - إضافة `Hotel_Id`
- `ReservationBoardOptions` - إضافة `Hotel_Id`

**جداول الغرف:**
- `Rooms` - إضافة `Hotel_Id`
- `RoomStatusHistories` - إضافة `Hotel_Id`

**جداول الأسعار:**
- `RateCodeHeaders` - إضافة `Hotel_Id`
- `RateCodeDetails` - إضافة `Hotel_Id`
- `Promotions` - إضافة `Hotel_Id`

**جداول نقاط البيع:**
- `Outlets` - إضافة `Hotel_Id`
- `PosTerminals` - إضافة `Hotel_Id`
- `Tables` - إضافة `Hotel_Id`
- `MenuArticles` - إضافة `Hotel_Id`
- `MenuLinks` - إضافة `Hotel_Id`

**جداول الحركات المالية:**
- `FinancialPostings` - إضافة `Hotel_Id`
- `Cashiers` - إضافة `Hotel_Id`
- `CashierStartingAmounts` - إضافة `Hotel_Id`

**جداول الإدارات:**
- `DepartmentCodes` - إضافة `Hotel_Id` (أو جدول مشترك)
- `HotelDepartments` - إضافة `Hotel_Id`

**جداول أخرى:**
- `LostAndFound` - إضافة `Hotel_Id`
- `UserActivities` - إضافة `Hotel_Id`
- `FiscalPrinterTransactions` - إضافة `Hotel_Id`
- `SystemParameters` - إضافة `Hotel_Id`

### الجداول المشتركة (لا تحتاج Hotel_Id)

هذه الجداول يمكن أن تكون مشتركة بين جميع الفنادق:

- `Countries` - الدول
- `States` - الولايات
- `Regions` - المناطق
- `Cities` - المدن
- `Currencies` - العملات
- `AddressTypes` - أنواع العناوين
- `CommunicationTypes` - أنوات الاتصال
- `RoomCategories` - فئات الغرف (مع إمكانية التخصيص لكل فندق)
- `PaymentTypes` - أنواع الدفع
- `TaxDescriptions` - أوصاف الضرائب

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

## 🎯 التوصيات النهائية

### 1. البنية التقنية المقترحة
- **قاعدة البيانات**: PostgreSQL (مجاني ومفتوح المصدر) أو SQL Server
- **الواجهة الخلفية**: .NET Core / Node.js / Python (Django/FastAPI)
- **الواجهة الأمامية**: React / Vue.js / Angular
- **المصادقة**: JWT مع Role-Based Access Control (RBAC)
- **API**: RESTful API

### 2. الأمان
- تشفير كلمات المرور (bcrypt/argon2)
- HTTPS لجميع الاتصالات
- Row-Level Security في قاعدة البيانات
- Audit Log لجميع العمليات الحساسة

### 3. المراقبة
- نظام مراقبة الأداء (Prometheus/Grafana)
- نظام تسجيل الأخطاء (Sentry/ELK)
- تنبيهات فورية للمشاكل

### 4. قابلية التوسع
- تصميم النظام ليقبل فنادق جديدة بسهولة
- نظام إدارة الإشتراكات
- نظام ترخيص مرن

---

## 📞 الخطوات التالية

1. **الموافقة على التصميم**: مراجعة هذا التحليل مع الإدارة
2. **اختيار البنية التقنية**: تحديد التقنيات المستخدمة
3. **تجهيز البيئة**: إعداد بيئة التطوير
4. **بدء التنفيذ**: البدء بالمرحلة 1

---

## 📝 الخلاصة

- ✅ **يمكن بناء نظام Multi-Tenant** بناءً على قاعدة البيانات الحالية
- ✅ **يحتاج 15 جدول جديد** لإدارة الفنادق والمستخدمين والصلاحيات
- ✅ **يحتاج تعديل 43 جدول** لإضافة Hotel_Id
- ✅ **النمط الموصى به**: Shared Database - Shared Schema

النظام المقترح سيوفر لـ Chain-Luxe منصة موحدة وفعالة لإدارة جميع فنادقها مع الحفاظ على عزل البيانات والمرونة في التخصيص.

---

**ملاحظة**: الخطة التنفيذية التفصيلية متوفرة في ملف منفصل: `Chain-Luxe_Implementation_Plan.md`

---

**تاريخ التحليل**: 14 سبتمبر 2026
**المحلل**: فريق تطوير Chain-Luxe
**الإصدار**: 1.0
