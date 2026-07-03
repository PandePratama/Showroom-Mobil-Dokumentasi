# Struktur Project Laravel 12 (Scalable Module-Based Architecture)
## Website Landing Page Showroom Mobil Bekas

## Arsitektur

Project menggunakan pendekatan:

- Laravel 12
- REST API
- Module Based Architecture
- Service Layer
- Repository Pattern (Opsional)
- Policy Authorization
- Form Request Validation
- API Resource
- JWT Authentication
- Redis Cache
- Cloudflare R2 Storage

Pendekatan ini bertujuan agar setiap modul bersifat **independen**, mudah diuji (testable), mudah dikembangkan, dan mudah dipelihara.

---

# Struktur Folder

```text
showroom-api/
│
├── app/
│   │
│   ├── Console/
│   ├── Exceptions/
│   ├── Helpers/
│   ├── Http/
│   │   ├── Middleware/
│   │   └── Controllers/
│   │
│   ├── Modules/
│   │
│   ├── Providers/
│   ├── Policies/
│   ├── Traits/
│   └── Support/
│
├── bootstrap/
├── config/
├── database/
│   ├── factories/
│   ├── migrations/
│   └── seeders/
│
├── routes/
│   ├── api.php
│   └── web.php
│
├── storage/
├── tests/
├── public/
└── vendor/
```

---

# Struktur Modules

```text
app/
└── Modules/
```

Setiap modul memiliki struktur yang sama.

---

# Contoh Module Product

```text
Modules/
└── Product/
    │
    ├── Controllers/
    │   └── ProductController.php
    │
    ├── Services/
    │   └── ProductService.php
    │
    ├── Requests/
    │   ├── StoreProductRequest.php
    │   └── UpdateProductRequest.php
    │
    ├── Resources/
    │   ├── ProductResource.php
    │   └── ProductCollection.php
    │
    ├── Policies/
    │   └── ProductPolicy.php
    │
    ├── Models/
    │   └── Product.php
    │
    ├── Repositories/
    │   ├── ProductRepository.php
    │   └── Contracts/
    │       └── ProductRepositoryInterface.php
    │
    ├── Routes/
    │   └── api.php
    │
    ├── Events/
    │
    ├── Listeners/
    │
    ├── Jobs/
    │
    ├── Actions/
    │
    ├── DTOs/
    │
    ├── Enums/
    │
    ├── Traits/
    │
    ├── Rules/
    │
    ├── Observers/
    │
    └── Tests/
```

---

# Struktur Seluruh Module

```text
Modules/
│
├── Authentication/
├── Dashboard/
├── User/
├── Role/
├── Permission/
├── Branch/
├── Brand/
├── CarModel/
├── Product/
├── ProductImage/
├── ProductVideo/
├── Banner/
├── CompanyProfile/
├── Setting/
├── SEO/
├── AuditLog/
└── Shared/
```

---

# Struktur Detail Setiap Module

```text
ModuleName/
│
├── Controllers/
│
├── Services/
│
├── Requests/
│
├── Resources/
│
├── Policies/
│
├── Models/
│
├── Repositories/
│
├── Routes/
│
├── DTOs/
│
├── Actions/
│
├── Traits/
│
├── Rules/
│
├── Enums/
│
├── Events/
│
├── Listeners/
│
├── Observers/
│
└── Tests/
```

---

# Penjelasan Folder

## Controllers

Bertugas menerima HTTP Request.

Tidak berisi Business Logic.

Contoh

```php
ProductController
BrandController
BranchController
```

Controller hanya memanggil Service.

---

## Services

Berisi seluruh Business Logic.

Contoh

```php
ProductService

create()

update()

publish()

feature()

delete()

search()
```

Service tidak mengetahui HTTP Request.

Service hanya fokus pada proses bisnis.

---

## Requests

Menggunakan Form Request Laravel.

Contoh

```php
StoreProductRequest

UpdateProductRequest
```

Seluruh validasi berada di sini.

---

## Resources

Mengubah Model menjadi JSON.

Contoh

```php
ProductResource

ProductCollection
```

Menghindari expose data yang tidak diperlukan.

---

## Policies

Mengatur Authorization.

Contoh

```php
view

create

update

delete

publish
```

Menggunakan Gate Laravel.

---

## Models

Berisi Entity Eloquent.

Contoh

```php
Product

Brand

Branch
```

Tidak berisi Business Logic.

---

## Repositories

Mengakses Database.

Contoh

```php
find()

findBySlug()

create()

update()

delete()
```

Jika suatu saat berpindah database, Service tidak berubah.

---

## Routes

Setiap module memiliki route sendiri.

Contoh

```php
Modules/Product/Routes/api.php
```

Kemudian diregister oleh RouteServiceProvider.

---

## DTO

Data Transfer Object.

Membawa data dari Controller ke Service.

---

## Actions

Untuk Business Process kecil.

Contoh

```php
UploadProductImageAction

PublishProductAction

GenerateSlugAction
```

---

## Rules

Custom Validation Rule.

Contoh

```php
UniqueSkuRule

UniqueSlugRule
```

---

## Traits

Trait reusable.

Contoh

```php
UploadFileTrait

UuidTrait

SearchableTrait
```

---

## Enums

PHP Native Enum.

Contoh

```php
TransmissionType

FuelType

PublishStatus
```

---

## Events

Contoh

```php
ProductCreated

ProductPublished
```

---

## Listeners

Contoh

```php
ClearRedisCache

WriteAuditLog
```

---

## Observers

Mengamati perubahan Model.

Contoh

```php
ProductObserver

BrandObserver
```

---

## Tests

Berisi

```text
Feature

Unit

Integration
```

---

# Shared Module

Digunakan bersama seluruh module.

```text
Shared/
│
├── Services/
├── DTOs/
├── Helpers/
├── Traits/
├── Rules/
├── Exceptions/
├── Resources/
└── Contracts/
```

---

# Contoh Alur Request

```text
HTTP Request
      │
      ▼
API Route
      │
      ▼
Controller
      │
      ▼
Form Request Validation
      │
      ▼
Policy Authorization
      │
      ▼
DTO
      │
      ▼
Service
      │
      ▼
Repository
      │
      ▼
Eloquent Model
      │
      ▼
MySQL
      │
      ▼
Resource
      │
      ▼
JSON Response
```

---

# Dependency Flow

```text
Controller
      │
      ▼
Service
      │
      ▼
Repository
      │
      ▼
Model
```

Aturan utama:

- Controller **tidak boleh** mengakses Model secara langsung.
- Controller **tidak boleh** berisi Business Logic.
- Service menjadi pusat seluruh aturan bisnis.
- Repository menjadi satu-satunya lapisan yang berinteraksi dengan database.
- Resource bertanggung jawab atas format respons API.

---

# Struktur Route

```text
routes/
│
├── api.php
└── web.php

app/
└── Modules/
    ├── Authentication/
    │   └── Routes/
    │       └── api.php
    │
    ├── Product/
    │   └── Routes/
    │       └── api.php
    │
    ├── Branch/
    │   └── Routes/
    │       └── api.php
    │
    └── ...
```

`routes/api.php` hanya bertugas memuat route dari setiap modul.

---

# Standar Penamaan

| Komponen | Format |
|----------|--------|
| Module | PascalCase (`Product`) |
| Controller | `ProductController` |
| Service | `ProductService` |
| Repository | `ProductRepository` |
| Interface | `ProductRepositoryInterface` |
| Request | `StoreProductRequest` |
| Resource | `ProductResource` |
| Policy | `ProductPolicy` |
| Model | `Product` |
| Observer | `ProductObserver` |
| Event | `ProductCreated` |
| Listener | `ClearProductCacheListener` |
| DTO | `CreateProductData` |
| Action | `PublishProductAction` |
| Enum | `PublishStatus` |

---

# Keunggulan Arsitektur

- Modular dan mudah dikembangkan.
- Setiap domain bisnis terisolasi dengan baik.
- Mendukung pengembangan oleh banyak developer secara paralel.
- Memudahkan unit testing dan integration testing.
- Business logic terpusat di Service Layer.
- Mudah menambahkan fitur baru tanpa memengaruhi modul lain.
- Siap dikembangkan menjadi sistem yang lebih besar seperti marketplace, ERP, atau aplikasi multi-tenant.
