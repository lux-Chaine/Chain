# خطة تنفيذ Chain-Luxe - التقنيات المختارة
## Svelte + Tailwind | .NET Core | PostgreSQL

---

## 🎯 التقنيات المختارة

| الطبقة | التقنية | السبب |
|--------|---------|-------|
| **Frontend** | SvelteKit + Tailwind CSS | أداء عالي، حجم صغير، تصميم سريع |
| **Backend** | ASP.NET Core 8 | أداء ممتاز، Strong Typing، Enterprise-ready |
| **Database** | PostgreSQL 15 | مجاني، RLS مدمج، JSON support |
| **ORM** | Entity Framework Core 8 | تكامل ممتاز مع .NET |
| **Caching** | Redis | أداء عالي للتخزين المؤقت |
| **Authentication** | JWT + ASP.NET Identity | أمان قوي، Standards-based |
| **API** | REST + WebSocket | Standard API + Real-time updates |

---

## 📅 نظرة عامة على الخطة

| المرحلة | الوصف | المدة الزمنية | الأولوية |
|---------|-------|---------------|-----------|
| المرحلة 1 | إعداد المشاريع والبيئة | 1 أسبوع | عالية جداً |
| المرحلة 2 | قاعدة البيانات و EF Core | 2 أسابيع | عالية جداً |
| المرحلة 3 | Backend Core APIs | 3 أسابيع | عالية |
| المرحلة 4 | Frontend Core UI | 3 أسابيع | عالية |
| المرحلة 5 | Authentication & Authorization | 2 أسابيع | عالية |
| المرحلة 6 | Advanced Features | 3 أسابيع | متوسطة |
| المرحلة 7 | الترحيل والبيانات | 2 أسابيع | عالية |
| المرحلة 8 | الاختبار والجودة | 2 أسابيع | متوسطة |
| المرحلة 9 | التدريب | 1 أسبوع | متوسطة |
| المرحلة 10 | الإطلاق | 1 أسبوع | عالية |

**المدة الإجمالية التقديرية**: 20 أسبوع (5 أشهر)

---

## 🎨 المرحلة 1: إعداد المشاريع والبيئة (1 أسبوع)

### 1.1 إعداد Repository Structure

```
chain-luxe/
├── frontend/          # SvelteKit + Tailwind
├── backend/           # ASP.NET Core Web API
├── database/          # SQL Scripts & Migrations
├── docker/            # Docker Compose files
└── docs/              # الوثائق
```

**المهام**:
- [ ] إنشاء Repository Git
- [ ] إنشاء هيكل المجلدات
- [ ] إعداد .gitignore لكل مشروع
- [ ] إعداد README لكل مشروع

**المسؤول**: DevOps Engineer
**المدة**: 1 يوم

### 1.2 إعداد Frontend (SvelteKit)

**المهام**:
- [ ] إنشاء مشروع SvelteKit: `npm create svelte@latest`
- [ ] إضافة TypeScript: `svelte-add ts`
- [ ] إضافة Tailwind CSS: `svelte-add tailwindcss`
- [ ] إعداد ESLint و Prettier
- [ ] إعداد environment variables
- [ ] إضافة مكتبات UI (Headless UI, Heroicons)
- [ ] إعداد PWA configuration

**المسؤول**: Frontend Developer
**المدة**: 2 يوم

**المخرجات**: مشروع SvelteKit جاهز مع Tailwind

### 1.3 إعداد Backend (.NET Core)

**المهام**:
- [ ] إنشاء Web API Project: `dotnet new webapi`
- [ ] إضافة Entity Framework Core: `dotnet add package Microsoft.EntityFrameworkCore`
- [ ] إضافة PostgreSQL provider: `dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL`
- [ ] إضافة JWT: `dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer`
- [ ] إضافة Swagger: `dotnet add package Swashbuckle.AspNetCore`
- [ ] إضافة CORS
- [ ] إعداد appsettings.json
- [ ] إضافة Health Checks

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: مشروع .NET Core Web API جاهز

### 1.4 إعداد Database (PostgreSQL)

**المهام**:
- [ ] تثبيت PostgreSQL 15 محلياً
- [ ] إنشاء قاعدة البيانات: `chainluxe_db`
- [ ] إنشاء Docker Compose للبيئة المحلية
- [ ] إعداد pgAdmin لقاعدة البيانات
- [ ] إنشاء connection string

**Docker Compose**:
```yaml
version: '3.8'
services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: chainluxe_db
      POSTGRES_USER: chainluxe
      POSTGRES_PASSWORD: your_password
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7
    ports:
      - "6379:6379"

volumes:
  postgres_data:
```

**المسؤول**: Database Developer
**المدة**: 1 يوم

**المخرجات**: قاعدة بيانات PostgreSQL جاهزة

### 1.5 إعداد CI/CD

**المهام**:
- [ ] إعداد GitHub Actions للـ Frontend
- [ ] إعداد GitHub Actions للـ Backend
- [ ] إعداد automated testing
- [ ] إعداد automated deployment

**المسؤول**: DevOps Engineer
**المدة**: 1 يوم

**المخرجات**: CI/CD Pipeline جاهز

---

## 🗄️ المرحلة 2: قاعدة البيانات و EF Core (2 أسابيع)

### 2.1 إنشاء DbContext من V8.dbml

**المهام**:
- [ ] تحويل V8.dbml إلى C# Classes
- [ ] إنشاء DbContext: `ChainLuxeDbContext`
- [ ] إضافة DbSets لكل جدول
- [ ] إضافة Relationships (Foreign Keys)
- [ ] إضافة Indexes على Hotel_Id
- [ ] إضافة Concurrency Tokens

**DbContext Example**:
```csharp
public class ChainLuxeDbContext : DbContext
{
    public DbSet<Hotel> Hotels { get; set; }
    public DbSet<Customer> Customers { get; set; }
    public DbSet<Reservation> Reservations { get; set; }
    // ... بقية الجداول

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        // إعدادات Multi-Tenant
        modelBuilder.Entity<Customer>()
            .HasQueryFilter(c => c.HotelId == GetCurrentHotelId());

        // Relationships
        modelBuilder.Entity<Customer>()
            .HasOne(c => c.Hotel)
            .WithMany(h => h.Customers)
            .HasForeignKey(c => c.HotelId);
    }

    private long GetCurrentHotelId()
    {
        // الحصول على Hotel_Id من HttpContext
        return _httpContextAccessor.HttpContext?
            .GetHotelId() ?? 0;
    }
}
```

**المسؤول**: Backend Developer
**المدة**: 3 أيام

**المخرجات**: DbContext جاهز

### 2.2 إنشاء Migrations

**المهام**:
- [ ] إنشاء Initial Migration: `dotnet ef migrations add InitialCreate`
- [ ] مراجعة Migration generated SQL
- [ ] تطبيق Migration: `dotnet ef database update`
- [ ] التحقق من الجداول في pgAdmin

**المسؤول**: Database Developer
**المدة**: 2 يوم

**المخرجات**: Migrations مطبقة

### 2.3 إعداد Row-Level Security (RLS)

**المهام**:
- [ ] إنشاء Policy لكل جدول يحتوي Hotel_Id
- [ ] إعداد Function للحصول على Hotel_Id الحالي
- [ ] تطبيق Policies على الجداول
- [ ] اختبار RLS بمستخدمين مختلفين

**SQL Example**:
```sql
-- Function للحصول على Hotel_Id
CREATE OR REPLACE FUNCTION get_current_hotel_id()
RETURNS bigint AS $$
BEGIN
    RETURN current_setting('app.current_hotel_id')::bigint;
END;
$$ LANGUAGE plpgsql;

-- Policy للعملاء
CREATE POLICY customer_hotel_isolation ON customers
FOR ALL
USING (hotel_id = get_current_hotel_id());

-- تفعيل RLS
ALTER TABLE customers ENABLE ROW LEVEL SECURITY;
```

**المسؤول**: Database Developer
**المدة**: 3 أيام

**المخرجات**: RLS مفعل ومختبر

### 2.4 Seed Data

**المهام**:
- [ ] إنشاء Seed Data للفنادق الثلاثة
- [ ] إنشاء Seed Data للأدوار الأساسية
- [ ] إنشاء Seed Data للمستخدمين Admin
- [ ] إنشاء Seed Data للبيانات المشتركة (Countries, Currencies, etc.)
- [ ] تطبيق Seed Data via EF Core

**Seed Data Example**:
```csharp
modelBuilder.Entity<Hotel>().HasData(
    new Hotel { Id = 1, Code = "AMON", Name = "فندق أمون", City = "الإسكندرية" },
    new Hotel { Id = 2, Code = "PALM", Name = "فندق بالم", City = "كفر الشيخ" },
    new Hotel { Id = 3, Code = "SIWA", Name = "فندق الوادي الجديد", City = "سيوة" }
);
```

**المسؤول**: Database Developer
**المدة**: 2 يوم

**المخرجات**: Seed Data مطبق

---

## ⚙️ المرحلة 3: Backend Core APIs (3 أسابيع)

### 3.1 إعداد Project Structure

```
backend/
├── Controllers/
│   ├── HotelsController.cs
│   ├── UsersController.cs
│   ├── CustomersController.cs
│   └── ReservationsController.cs
├── Services/
│   ├── IHotelService.cs
│   ├── HotelService.cs
│   └── ...
├── Models/
│   ├── DTOs/
│   └── Entities/
├── Middleware/
│   └── HotelMiddleware.cs
└── Program.cs
```

**المسؤول**: Backend Developer
**المدة**: 1 يوم

### 3.2 Hotels API

**المهام**:
- [ ] GET /api/hotels - قائمة الفنادق
- [ ] GET /api/hotels/{id} - تفاصيل فندق
- [ ] POST /api/hotels - إضافة فندق
- [ ] PUT /api/hotels/{id} - تعديل فندق
- [ ] DELETE /api/hotels/{id} - حذف فندق
- [ ] GET /api/hotels/{id}/settings - إعدادات الفندق

**Controller Example**:
```csharp
[ApiController]
[Route("api/[controller]")]
public class HotelsController : ControllerBase
{
    private readonly IHotelService _hotelService;

    [HttpGet]
    [Authorize]
    public async Task<ActionResult<IEnumerable<HotelDto>>> GetHotels()
    {
        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        var hotels = await _hotelService.GetUserHotelsAsync(userId);
        return Ok(hotels);
    }

    [HttpGet("{id}")]
    [Authorize]
    public async Task<ActionResult<HotelDto>> GetHotel(int id)
    {
        var hotel = await _hotelService.GetHotelByIdAsync(id);
        if (hotel == null) return NotFound();
        return Ok(hotel);
    }
}
```

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: Hotels API جاهز

### 3.3 Users & Authentication API

**المهام**:
- [ ] POST /api/auth/login - تسجيل الدخول
- [ ] POST /api/auth/register - تسجيل مستخدم جديد
- [ ] POST /api/auth/refresh - تجديد Token
- [ ] POST /api/auth/logout - تسجيل الخروج
- [ ] GET /api/users - قائمة المستخدمين
- [ ] POST /api/users - إضافة مستخدم
- [ ] PUT /api/users/{id} - تعديل مستخدم
- [ ] DELETE /api/users/{id} - حذف مستخدم

**Authentication Service**:
```csharp
public class AuthService : IAuthService
{
    public async Task<AuthResponse> LoginAsync(LoginRequest request)
    {
        var user = await _userManager.FindByEmailAsync(request.Email);
        if (user == null) return new AuthResponse { Success = false };

        var result = await _signInManager.CheckPasswordSignInAsync(user, request.Password, false);
        if (!result.Succeeded) return new AuthResponse { Success = false };

        var token = GenerateJwtToken(user);
        return new AuthResponse { Success = true, Token = token };
    }

    private string GenerateJwtToken(ApplicationUser user)
    {
        var claims = new[]
        {
            new Claim(ClaimTypes.NameIdentifier, user.Id),
            new Claim(ClaimTypes.Email, user.Email),
            new Claim("HotelId", user.HotelId.ToString())
        };

        var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_configuration["Jwt:Key"]));
        var creds = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);

        var token = new JwtSecurityToken(
            claims: claims,
            expires: DateTime.Now.AddDays(7),
            signingCredentials: creds
        );

        return new JwtSecurityTokenHandler().WriteToken(token);
    }
}
```

**المسؤول**: Backend Developer
**المدة**: 3 أيام

**المخرجات**: Authentication API جاهز

### 3.4 Customers API

**المهام**:
- [ ] GET /api/customers - قائمة العملاء (مع Filter حسب Hotel)
- [ ] GET /api/customers/{id} - تفاصيل عميل
- [ ] POST /api/customers - إضافة عميل
- [ ] PUT /api/customers/{id} - تعديل عميل
- [ ] DELETE /api/customers/{id} - حذف عميل
- [ ] GET /api/customers/search - بحث في العملاء
- [ ] GET /api/customers/{id}/addresses - عناوين العميل
- [ ] GET /api/customers/{id}/communications - اتصالات العميل

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: Customers API جاهز

### 3.5 Reservations API

**المهام**:
- [ ] GET /api/reservations - قائمة الحجوزات
- [ ] GET /api/reservations/{id} - تفاصيل حجز
- [ ] POST /api/reservations - إنشاء حجز
- [ ] PUT /api/reservations/{id} - تعديل حجز
- [ ] DELETE /api/reservations/{id} - حذف حجز
- [ ] POST /api/reservations/{id}/checkin - تسجيل وصول
- [ ] POST /api/reservations/{id}/checkout - تسجيل مغادرة
- [ ] GET /api/reservations/availability - التحقق من التوفر

**Reservation Service**:
```csharp
public class ReservationService : IReservationService
{
    public async Task<ReservationDto> CreateReservationAsync(CreateReservationRequest request)
    {
        var reservation = new Reservation
        {
            HotelId = GetCurrentHotelId(),
            GuestProfileId = request.GuestProfileId,
            ExpectedArrival = request.ExpectedArrival,
            ExpectedDeparture = request.ExpectedDeparture,
            // ... بقية الحقول
        };

        _context.Reservations.Add(reservation);
        await _context.SaveChangesAsync();

        return _mapper.Map<ReservationDto>(reservation);
    }

    public async Task<bool> CheckAvailabilityAsync(int roomCategoryId, DateTime checkIn, DateTime checkOut)
    {
        var hotelId = GetCurrentHotelId();
        var availableRooms = await _context.Rooms
            .Where(r => r.HotelId == hotelId && r.RoomCategoryId == roomCategoryId)
            .Where(r => !_context.Reservations
                .Any(res => res.RoomId == r.Id &&
                          res.ExpectedArrival < checkOut &&
                          res.ExpectedDeparture > checkIn))
            .CountAsync();

        return availableRooms > 0;
    }
}
```

**المسؤول**: Backend Developer
**المدة**: 3 أيام

**المخرجات**: Reservations API جاهز

### 3.6 Rooms API

**المهام**:
- [ ] GET /api/rooms - قائمة الغرف
- [ ] GET /api/rooms/{id} - تفاصيل غرفة
- [ ] PUT /api/rooms/{id}/status - تغيير حالة الغرفة
- [ ] GET /api/rooms/rack - Room Rack
- [ ] GET /api/rooms/map - Room Map

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: Rooms API جاهز

### 3.7 Invoices API

**المهام**:
- [ ] GET /api/invoices - قائمة الفواتير
- [ ] GET /api/invoices/{id} - تفاصيل فاتورة
- [ ] POST /api/invoices - إنشاء فاتورة
- [ ] POST /api/invoices/{id}/print - طباعة فاتورة
- [ ] GET /api/invoices/{id}/pdf - تصدير PDF

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: Invoices API جاهز

---

## 🎨 المرحلة 4: Frontend Core UI (3 أسابيع)

### 4.1 إعداد Project Structure

```
frontend/
├── src/
│   ├── lib/
│   │   ├── components/
│   │   ├── stores/
│   │   ├── services/
│   │   └── types/
│   ├── routes/
│   └── app.html
└── static/
```

**المسؤول**: Frontend Developer
**المدة**: 1 يوم

### 4.2 إنشاء Layout و Components المشتركة

**المهام**:
- [ ] إنشاء Layout الرئيسي
- [ ] إنشاء Navbar
- [ ] إنشاء Sidebar
- [ ] إنشاء Footer
- [ ] إنشاء Loading Spinner
- [ ] إنشاء Error Boundary
- [ ] إنشاء Toast Notifications

**Layout Example**:
```svelte
<script lang="ts">
  import { page } from '$app/stores';
  import { hotelStore } from '$lib/stores/hotel';
  import Navbar from '$lib/components/Navbar.svelte';
  import Sidebar from '$lib/components/Sidebar.svelte';

  $: currentHotel = hotelStore.current;
</script>

<svelte:head>
  <title>{$page.data.title} - Chain-Luxe</title>
</svelte:head>

<div class="min-h-screen bg-gray-100">
  <Navbar />
  <div class="flex">
    <Sidebar />
    <main class="flex-1 p-6">
      <slot />
    </main>
  </div>
</div>
```

**المسؤول**: Frontend Developer
**المدة**: 2 يوم

**المخرجات**: Layout و Components جاهزة

### 4.3 Authentication UI

**المهام**:
- [ ] صفحة تسجيل الدخول (Login)
- [ ] اختيار الفندق في تسجيل الدخول
- [ ] صفحة تسجيل مستخدم جديد (Register)
- [ ] صفحة نسيان كلمة المرور (Forgot Password)
- [ ] إدارة JWT Token
- [ ] Auto-refresh Token
- [ ] Logout

**Login Page Example**:
```svelte
<script lang="ts">
  import { goto } from '$app/navigation';
  import { authStore } from '$lib/stores/auth';
  import { hotelStore } from '$lib/stores/hotel';

  let email = '';
  let password = '';
  let selectedHotel = 1;
  let hotels = [];

  onMount(async () => {
    hotels = await hotelStore.getHotels();
  });

  async function handleLogin() {
    const success = await authStore.login(email, password, selectedHotel);
    if (success) {
      goto('/dashboard');
    }
  }
</script>

<div class="min-h-screen flex items-center justify-center bg-gray-100">
  <div class="bg-white p-8 rounded-lg shadow-md w-96">
    <h1 class="text-2xl font-bold mb-6 text-center">تسجيل الدخول</h1>

    <form on:submit|preventDefault={handleLogin}>
      <div class="mb-4">
        <label class="block text-gray-700 mb-2">البريد الإلكتروني</label>
        <input
          type="email"
          bind:value={email}
          class="w-full px-3 py-2 border rounded"
          required
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700 mb-2">كلمة المرور</label>
        <input
          type="password"
          bind:value={password}
          class="w-full px-3 py-2 border rounded"
          required
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700 mb-2">الفندق</label>
        <select bind:value={selectedHotel} class="w-full px-3 py-2 border rounded">
          {#each hotels as hotel}
            <option value={hotel.id}>{hotel.name}</option>
          {/each}
        </select>
      </div>

      <button
        type="submit"
        class="w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700"
      >
        تسجيل الدخول
      </button>
    </form>
  </div>
</div>
```

**المسؤول**: Frontend Developer
**المدة**: 2 يوم

**المخرجات**: Authentication UI جاهز

### 4.4 Dashboard UI

**المهام**:
- [ ] صفحة Dashboard الرئيسية
- [ ] إحصائيات عامة (عدد الحجوزات، الإشغال، الإيرادات)
- [ ] رسوم بيانية (Charts)
- [ ] Recent Activities
- [ ] Quick Actions
- [ ] Hotel Selector

**Dashboard Example**:
```svelte
<script lang="ts">
  import { onMount } from 'svelte';
  import { hotelStore } from '$lib/stores/hotel';
  import DashboardStats from '$lib/components/DashboardStats.svelte';
  import RecentActivities from '$lib/components/RecentActivities.svelte';

  let stats = {
    totalReservations: 0,
    occupancyRate: 0,
    revenue: 0,
    checkIns: 0,
    checkOuts: 0
  };

  onMount(async () => {
    stats = await fetchStats();
  });

  async function fetchStats() {
    const response = await fetch('/api/dashboard/stats');
    return await response.json();
  }
</script>

<div class="p-6">
  <h1 class="text-3xl font-bold mb-6">لوحة التحكم</h1>

  <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-6">
    <DashboardStats label="إجمالي الحجوزات" value={stats.totalReservations} />
    <DashboardStats label="نسبة الإشغال" value={`${stats.occupancyRate}%`} />
    <DashboardStats label="الإيرادات" value={`${stats.revenue} EGP`} />
    <DashboardStats label="تسجيلات الوصول" value={stats.checkIns} />
  </div>

  <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
    <RecentActivities />
    <!-- بقية الـ Widgets -->
  </div>
</div>
```

**المسؤول**: Frontend Developer
**المدة**: 3 أيام

**المخرجات**: Dashboard UI جاهز

### 4.5 Hotels Management UI

**المهام**:
- [ ] قائمة الفنادق
- [ ] إضافة/تعديل فندق
- [ ] إعدادات الفندق
- [ ] إدارة أنواع الغرف لكل فندق
- [ ] إدارة الأقسام لكل فندق

**المسؤول**: Frontend Developer
**المدة**: 2 يوم

**المخرجات**: Hotels Management UI جاهز

### 4.6 Customers Management UI

**المهام**:
- [ ] قائمة العملاء
- [ ] إضافة/تعديل عميل
- [ ] تفاصيل العميل
- [ ] العناوين والاتصالات
- [ ] البحث والتصفية
- [ ] ملاحظات العميل

**المسؤول**: Frontend Developer
**المدة**: 3 أيام

**المخرجات**: Customers Management UI جاهز

### 4.7 Reservations Management UI

**المهام**:
- [ ] قائمة الحجوزات
- [ ] إنشاء حجز جديد
- [ ] تفاصيل الحجز
- [ ] تعديل الحجز
- [ ] إلغاء الحجز
- [ ] Check-in / Check-out
- [ ] Timeline للحجز
- [ ] التقويم المرئي

**المسؤول**: Frontend Developer
**المدة**: 4 أيام

**المخرجات**: Reservations Management UI جاهز

---

## 🔐 المرحلة 5: Authentication & Authorization (2 أسابيع)

### 5.1 JWT Implementation (Backend)

**المهام**:
- [ ] إعداد JWT Configuration
- [ ] إنشاء JWT Token Generator
- [ ] إنشاء JWT Token Validator
- [ ] إعداد Refresh Token Mechanism
- [ ] إعداد Token Expiration

**appsettings.json**:
```json
{
  "Jwt": {
    "Key": "your-super-secret-key-min-32-chars",
    "Issuer": "ChainLuxe",
    "Audience": "ChainLuxeUsers",
    "ExpiryInMinutes": 60
  }
}
```

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: JWT Implementation جاهز

### 5.2 Role-Based Access Control (RBAC)

**المهام**:
- [ ] تعريف الأدوار (Admin, Manager, Receptionist, etc.)
- [ ] تعريف الصلاحيات (Permissions)
- [ ] ربط الأدور بالصلاحيات
- [ ] إنشاء Policy-based Authorization
- [ ] تطبيق Authorization على Controllers

**Authorization Policy Example**:
```csharp
public static class Policies
{
    public const string CanManageHotels = "CanManageHotels";
    public const string CanManageReservations = "CanManageReservations";
    public const string CanManageCustomers = "CanManageCustomers";
}

// في Program.cs
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy(Policies.CanManageHotels, policy =>
        policy.RequireRole("Admin"));
    options.AddPolicy(Policies.CanManageReservations, policy =>
        policy.RequireClaim("Permission", "ManageReservations"));
});
```

**المسؤول**: Backend Developer
**المدة**: 3 أيام

**المخرجات**: RBAC جاهز

### 5.3 Hotel Access Control

**المهام**:
- [ ] إعداد Hotel Selection Middleware
- [ ] إعداد Hotel ID Validation
- [ ] إعداد Hotel-based Authorization
- [ ] اختبار وصول المستخدم لفنادق متعددة

**Hotel Middleware**:
```csharp
public class HotelMiddleware
{
    private readonly RequestDelegate _next;

    public HotelMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        var hotelId = context.Request.Headers["X-Hotel-Id"].FirstOrDefault();
        if (!string.IsNullOrEmpty(hotelId))
        {
            context.Items["HotelId"] = hotelId;
        }

        await _next(context);
    }
}
```

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: Hotel Access Control جاهز

### 5.4 Permission Management UI (Frontend)

**المهام**:
- [ ] صفحة إدارة الأدوار
- [ ] صفحة إدارة الصلاحيات
- [ ] ربط الصلاحيات بالأدوار
- [ ] تعيين أدوار للمستخدمين
- [ ] تعيين وصول المستخدم للفنادق

**المسؤول**: Frontend Developer
**المدة**: 3 أيام

**المخرجات**: Permission Management UI جاهز

---

## 🚀 المرحلة 6: Advanced Features (3 أسابيع)

### 6.1 Real-time Updates (WebSocket)

**المهام**:
- [ ] إعداد SignalR في .NET
- [ ] إنشاء Hubs للحجوزات والغرف
- [ ] إنشاء WebSocket Client في Svelte
- [ ] إعداد Real-time Dashboard
- [ ] إعداد Real-time Room Rack

**SignalR Hub Example**:
```csharp
public class ReservationHub : Hub
{
    public async Task JoinHotelGroup(string hotelId)
    {
        await Groups.AddToGroupAsync(Context.ConnectionId, $"hotel_{hotelId}");
    }

    public async Task ReservationCreated(int hotelId, ReservationDto reservation)
    {
        await Clients.Group($"hotel_{hotelId}")
            .SendAsync("ReservationCreated", reservation);
    }
}
```

**Svelte WebSocket Client**:
```svelte
<script lang="ts">
  import { onMount, onDestroy } from 'svelte';

  let connection: WebSocket;
  let notifications = [];

  onMount(() => {
    connection = new WebSocket('ws://localhost:5000/reservationhub');

    connection.onmessage = (event) => {
      const data = JSON.parse(event.data);
      if (data.type === 'ReservationCreated') {
        notifications = [...notifications, data];
      }
    };
  });

  onDestroy(() => {
    connection.close();
  });
</script>
```

**المسؤول**: Backend Developer (2 يوم) + Frontend Developer (2 يوم)
**المدة**: 4 أيام

**المخرجات**: Real-time Updates جاهز

### 6.2 Caching (Redis)

**المهام**:
- [ ] إعداد Redis Docker container
- [ ] إضافة StackExchange.Redis في .NET
- [ ] إنشاء Cache Service
- [ ] Cache للبيانات المشتركة (Countries, Currencies)
- [ ] Cache للإعدادات الفندق
- [ ] Cache للإحصائيات

**Cache Service Example**:
```csharp
public class CacheService : ICacheService
{
    private readonly IDatabase _database;

    public CacheService(IConnectionMultiplexer redis)
    {
        _database = redis.GetDatabase();
    }

    public async Task<T> GetAsync<T>(string key)
    {
        var value = await _database.StringGetAsync(key);
        return value.HasValue ? JsonSerializer.Deserialize<T>(value) : default;
    }

    public async Task SetAsync<T>(string key, T value, TimeSpan? expiry = null)
    {
        var serialized = JsonSerializer.Serialize(value);
        await _database.StringSetAsync(key, serialized, expiry);
    }
}
```

**المسؤول**: Backend Developer
**المدة**: 2 يوم

**المخرجات**: Caching جاهز

### 6.3 File Upload (Images/Documents)

**المهام**:
- [ ] إعداد File Upload API
- [ ] إعداد Azure Blob Storage أو Local Storage
- [ ] رفع شعارات الفنادق
- [ ] رفع وثائق العملاء
- [ ] رفع صور الغرف
- [ ] Image Optimization

**المسؤول**: Backend Developer (2 يوم) + Frontend Developer (1 يوم)
**المدة**: 3 أيام

**المخرجات**: File Upload جاهز

### 6.4 Reporting & Exports

**المهام**:
- [ ] إنشاء Reports API
- [ ] إعداد PDF Generation (iTextSharp or QuestPDF)
- [ ] إعداد Excel Export (EPPlus or ClosedXML)
- [ ] تقارير الحجوزات
- [ ] تقارير الإيرادات
- [ ] تقارير الإشغال

**المسؤول**: Backend Developer
**المدة**: 3 أيام

**المخرجات**: Reporting & Exports جاهز

### 6.5 Notifications System

**المهام**:
- [ ] إنشاء Notifications API
- [ ] إعداد Email Notifications (SendGrid)
- [ ] إعداد SMS Notifications (Twilio)
- [ ] إعداد In-App Notifications
- [ ] إعداد Push Notifications (Firebase)

**المسؤول**: Backend Developer
**المدة**: 3 أيام

**المخرجات**: Notifications System جاهز

---

## 📊 المرحلة 7: الترحيل والبيانات (2 أسابيع)

### 7.1 تحليل البيانات القديمة

**المهام**:
- [ ] فحص قاعدة البيانات Oracle القديمة
- [ ] تحديد الجداول المراد ترحيلها
- [ ] تحديد العلاقات
- [ ] إنشاء Mapping Document

**المسؤول**: Database Developer
**المدة**: 3 أيام

**المخرجات**: Mapping Document جاهز

### 7.2 إنشاء Migration Scripts

**المهام**:
- [ ] إنشاء Script للتصدير من Oracle
- [ ] إنشاء Script للاستيراد إلى PostgreSQL
- [ ] إنشاء Script لتعيين Hotel_Id
- [ ] إنشاء Script للتحقق من البيانات

**المسؤول**: Database Developer
**المدة**: 4 أيام

**المخرجات**: Migration Scripts جاهزة

### 7.3 ترحيل البيانات

**المهام**:
- [ ] ترحيل البيانات المشتركة
- [ ] ترحيل بيانات فندق أمون (Hotel_Id = 1)
- [ ] ترحيل بيانات فندق بالم (Hotel_Id = 2)
- [ ] ترحيل بيانات فندق سيوة (Hotel_Id = 3)
- [ ] التحقق من صحة البيانات

**المسؤول**: Database Developer
**المدة**: 5 أيام

**المخرجات**: البيانات مُرحلة

### 7.4 Data Validation

**المهام**:
- [ ] التحقق من اكتمال البيانات
- [ ] التحقق من صحة العلاقات
- [ ] التحقق من تعيين Hotel_Id
- [ ] إصلاح الأخطاء

**المسؤول**: Database Developer
**المدة**: 2 يوم

**المخرجات**: بيانات صحيحة وجاهزة

---

## 🧪 المرحلة 8: الاختبار والجودة (2 أسابيع)

### 8.1 Unit Testing

**المهام**:
- [ ] Unit Tests للـ Backend (xUnit)
- [ ] Unit Tests للـ Frontend (Vitest)
- [ ] اختبار جميع الـ Services
- [ ] اختبار جميع الـ Components

**xUnit Example**:
```csharp
public class HotelServiceTests
{
    [Fact]
    public async Task GetHotelById_ShouldReturnHotel()
    {
        // Arrange
        var mockRepository = new Mock<IHotelRepository>();
        var service = new HotelService(mockRepository.Object);

        // Act
        var result = await service.GetHotelByIdAsync(1);

        // Assert
        Assert.NotNull(result);
        Assert.Equal(1, result.Id);
    }
}
```

**المسؤول**: Backend Developer + Frontend Developer
**المدة**: 3 أيام

**المخرجات**: Unit Tests جاهزة

### 8.2 Integration Testing

**المهام**:
- [ ] Integration Tests للـ API
- [ ] اختبار Database Queries
- [ ] اختبار Authentication & Authorization
- [ ] اختبار Multi-Tenant Isolation

**المسؤول**: QA Engineer
**المدة**: 3 أيام

**المخرجات**: Integration Tests جاهزة

### 8.3 System Testing

**المهام**:
- [ ] اختبار سير العمل (Workflows)
- [ ] اختبار Check-in / Check-out
- [ ] اختبار إنشاء الحجوزات
- [ ] اختبار الفواتير
- [ ] اختبار نقاط البيع

**المسؤول**: QA Engineer
**المدة**: 3 أيام

**المخرجات**: System Tests جاهزة

### 8.4 Performance Testing

**المهام**:
- [ ] Load Testing (k6 or JMeter)
- [ ] Stress Testing
- [ ] Database Performance Testing
- [ ] API Response Time Testing
- [ ] تحسين الأداء

**المسؤول**: DevOps Engineer
**المدة**: 2 يوم

**المخرجات**: Performance Report جاهز

### 8.5 Security Testing

**المهام**:
- [ ] SQL Injection Testing
- [ ] XSS Testing
- [ ] CSRF Testing
- [ ] Authentication Testing
- [ ] Authorization Testing
- [ ] Penetration Testing

**المسؤول**: Security Engineer
**المدة**: 2 يوم

**المخرجات**: Security Report جاهز

---

## 🎓 المرحلة 9: التدريب (1 أسبوع)

### 9.1 إعداد مواد التدريب

**المهام**:
- [ ] كتابة User Manual
- [ ] كتابة Admin Manual
- [ ] إنشاء Video Tutorials
- [ ] إنشاء Quick Start Guide
- [ ] إنشاء FAQ

**المسؤول**: Technical Writer
**المدة**: 2 يوم

**المخرجات**: مواد تدريبية جاهزة

### 9.2 تدريب الإداريين

**المهام**:
- [ ] تدريب على Dashboard
- [ ] تدريب على التقارير
- [ ] تدريب على إدارة المستخدمين
- [ ] تدريب على إعدادات الفندق

**المسؤول**: Project Manager
**المدة**: 1 يوم

**المخرجات**: إداريون مدربون

### 9.3 تدريب موظفي الاستقبال

**المهام**:
- [ ] تدريب على إدارة الحجوزات
- [ ] تدريب على Check-in / Check-out
- [ ] تدريب على إدارة الغرف
- [ ] تدريب على الفواتير

**المسؤول**: Project Manager
**المدة**: 2 يوم

**المخرجات**: موظفو استقبال مدربون

### 9.4 تدريب موظفي الحسابات

**المهام**:
- [ ] تدريب على الفواتير
- [ ] تدريب على الحركات المالية
- [ ] تدريب على التقارير المالية

**المسؤول**: Project Manager
**المدة**: 1 يوم

**المخرجات**: موظفو حسابات مدربون

---

## 🚀 المرحلة 10: الإطلاق (1 أسبوع)

### 10.1 التحضير للإطلاق

**المهام**:
- [ ] النهائي Backup
- [ ] إعداد Production Server
- [ ] تكوين PostgreSQL Production
- [ ] تكوين SSL Certificate
- [ ] تكوين Domain/DNS
- [ ] إعداد Monitoring
- [ ] إعداد Logging

**المسؤول**: DevOps Engineer
**المدة**: 2 يوم

**المخرجات**: بيئة إنتاج جاهزة

### 10.2 النشر

**المهام**:
- [ ] نشر Backend (Azure App Service أو VPS)
- [ ] نشر Frontend (Vercel أو Netlify)
- [ ] نشر Database (Azure Database أو RDS)
- [ ] تكوين Environment Variables
- [ ] تشغيل Migrations
- [ ] اختبار Smoke Test

**Docker for Production**:
```yaml
version: '3.8'
services:
  backend:
    build: ./backend
    environment:
      - ASPNETCORE_ENVIRONMENT=Production
      - ConnectionStrings__DefaultConnection=${DB_CONNECTION_STRING}
    depends_on:
      - postgres
      - redis

  frontend:
    build: ./frontend
    environment:
      - VITE_API_URL=${API_URL}

  postgres:
    image: postgres:15
    environment:
      - POSTGRES_DB=${DB_NAME}
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_PASSWORD=${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine

volumes:
  postgres_data:
```

**المسؤول**: DevOps Engineer
**المدة**: 2 يوم

**المخرجات**: النظام منشور

### 10.3 إطلاق تدريجي

**المهام**:
- [ ] إطلاق لفندق أمون
- [ ] مراقبة الأخطاء
- [ ] دعم المستخدمين
- [ ] إطلاق لفندق بالم
- [ ] إطلاق لفندق سيوة

**المسؤول**: Project Manager + Support Team
**المدة**: 3 يوم

**المخرجات**: جميع الفنادق تعمل

---

## 👥 الفريق المطلوب

| الدور | العدد | الدوام |
|------|-------|--------|
| Project Manager | 1 | دوام كامل |
| Technical Lead | 1 | دوام كامل |
| Backend Developer (.NET) | 2 | دوام كامل |
| Frontend Developer (Svelte) | 2 | دوام كامل |
| Database Developer | 1 | دوام كامل |
| DevOps Engineer | 1 | نصف دوام |
| QA Engineer | 1 | دوام كامل |
| UI/UX Designer | 1 | نصف دوام |
| Security Engineer | 1 | نصف دوام |

**إجمالي الفريق**: 10 شخص

---

## 💰 الميزانية التقديرية

### الرواتب (5 أشهر)
| الدور | الشهري | الإجمالي |
|-------|-------|---------|
| Project Manager | $3,000 | $15,000 |
| Technical Lead | $4,000 | $20,000 |
| Backend Developer (2x) | $2,500 | $25,000 |
| Frontend Developer (2x) | $2,500 | $25,000 |
| Database Developer | $2,500 | $12,500 |
| DevOps Engineer | $2,000 | $10,000 |
| QA Engineer | $2,000 | $10,000 |
| Security Engineer | $2,000 | $10,000 |
| UI/UX Designer | $1,500 | $7,500 |
| **الإجمالي** | - | **$135,000** |

### البنية التحتية (5 أشهر)
| البند | الشهري | الإجمالي |
|-------|-------|---------|
| Azure App Service | $200 | $1,000 |
| Azure Database | $150 | $750 |
| Vercel (Frontend) | $20 | $100 |
| Redis | $50 | $250 |
| Domain & SSL | $10 | $50 |
| Monitoring Tools | $50 | $250 |
| **الإجمالي** | - | **$2,400** |

### البرمجيات والتراخيص
| البند | التكلفة |
|-------|---------|
| Azure DevOps | مجاني |
| GitHub | مجاني |
| PostgreSQL | مجاني |
| **الإجمالي** | **$0** |

### الميزانية الإجمالية
| الفئة | المبلغ |
|-------|--------|
| الرواتب | $135,000 |
| البنية التحتية | $2,400 |
| البرمجيات | $0 |
| **الإجمالي** | **$137,400** |

---

## 📝 معايير النجاح

### معايير النجاح الأساسية
1. ✅ إطلاق النظام في الموعد المحدد
2. ✅ ترحيل جميع البيانات بنجاح
3. ✅ عدم وجود أخطاء حرجة بعد الإطلاق
4. ✅ رضا المستخدمين (80%+)
5. ✅ أداء النظام مقبول (<2s response time)

### معايير النجاح الثانوية
1. ✅ تقليل وقت التشغيل اليدوي بنسبة 50%
2. ✅ زيادة دقة البيانات بنسبة 90%
3. ✅ تقليل الأخطاء البشرية بنسبة 70%
4. ✅ تحسين تجربة المستخدم

---

## 🎯 التوصيات النهائية

### 1. البنية التقنية
- ✅ **Frontend**: SvelteKit + Tailwind CSS
- ✅ **Backend**: ASP.NET Core 8
- ✅ **Database**: PostgreSQL 15
- ✅ **ORM**: Entity Framework Core 8
- ✅ **Caching**: Redis
- ✅ **Authentication**: JWT + ASP.NET Identity

### 2. الأمان
- ✅ تشفير كلمات المرور (ASP.NET Identity)
- ✅ HTTPS لجميع الاتصالات
- ✅ Row-Level Security في PostgreSQL
- ✅ Audit Log لجميع العمليات الحساسة
- ✅ Rate Limiting للـ API

### 3. المراقبة
- ✅ Azure Monitor (للـ .NET)
- ✅ Application Insights
- ✅ Sentry (للـ Frontend)
- ✅ pg_stat_statements (للـ PostgreSQL)

### 4. قابلية التوسع
- ✅ Horizontal Scaling (Azure App Service)
- ✅ Database Partitioning (PostgreSQL)
- ✅ Load Balancing (Azure Load Balancer)

---

## 📞 الخطوات التالية الفورية

1. ✅ **اختيار التقنيات**: تم (Svelte, .NET, PostgreSQL)
2. ⏳ **إنشاء Repository Structure**: يجب البدء
3. ⏳ **إعداد المشاريع**: يجب البدء
4. ⏳ **إعداد البيئة المحلية**: يجب البدء

---

**تاريخ إنشاء الخطة**: 14 سبتمبر 2026
**الإصدار**: 2.0
**الحالة**: جاهزة للتنفيذ
