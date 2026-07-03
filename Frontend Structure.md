# Struktur Project Next.js (Feature-Based Architecture)
## Website Landing Page Showroom Mobil Bekas

## Teknologi

- Next.js 15+
- React
- TypeScript
- App Router
- Tailwind CSS
- Shadcn UI
- Axios
- TanStack Query
- React Hook Form
- Zod

---

# Struktur Folder

```text
showroom-frontend/
│
├── app/
│   ├── (public)/
│   │   ├── page.tsx
│   │   ├── about/
│   │   ├── contact/
│   │   ├── products/
│   │   │   ├── page.tsx
│   │   │   └── [slug]/
│   │   │       └── page.tsx
│   │   └── search/
│   │       └── page.tsx
│   │
│   ├── (dashboard)/
│   │   ├── dashboard/
│   │   ├── users/
│   │   ├── roles/
│   │   ├── permissions/
│   │   ├── branches/
│   │   ├── brands/
│   │   ├── car-models/
│   │   ├── products/
│   │   ├── banners/
│   │   ├── settings/
│   │   ├── audit-logs/
│   │   └── company-profile/
│   │
│   ├── login/
│   │   └── page.tsx
│   │
│   ├── layout.tsx
│   ├── loading.tsx
│   ├── not-found.tsx
│   ├── error.tsx
│   └── globals.css
│
├── components/
│   ├── ui/
│   ├── layouts/
│   ├── tables/
│   ├── forms/
│   ├── dialogs/
│   ├── cards/
│   ├── charts/
│   ├── breadcrumbs/
│   ├── pagination/
│   ├── uploader/
│   ├── seo/
│   └── common/
│
├── features/
│   ├── auth/
│   │   ├── api/
│   │   ├── hooks/
│   │   ├── components/
│   │   ├── types/
│   │   ├── validation/
│   │   └── services/
│   │
│   ├── dashboard/
│   ├── users/
│   ├── roles/
│   ├── permissions/
│   ├── branches/
│   ├── brands/
│   ├── car-models/
│   ├── products/
│   │   ├── api/
│   │   ├── hooks/
│   │   ├── components/
│   │   ├── forms/
│   │   ├── validation/
│   │   ├── services/
│   │   ├── types/
│   │   └── utils/
│   │
│   ├── product-images/
│   ├── product-videos/
│   ├── banners/
│   ├── company-profile/
│   ├── settings/
│   ├── audit-logs/
│   └── seo/
│
├── hooks/
│   ├── use-auth.ts
│   ├── use-pagination.ts
│   ├── use-debounce.ts
│   ├── use-confirm.ts
│   ├── use-upload.ts
│   ├── use-search.ts
│   └── use-table.ts
│
├── services/
│   ├── api.ts
│   ├── axios.ts
│   ├── auth.service.ts
│   ├── upload.service.ts
│   └── storage.service.ts
│
├── providers/
│   ├── auth-provider.tsx
│   ├── query-provider.tsx
│   ├── theme-provider.tsx
│   ├── permission-provider.tsx
│   └── toast-provider.tsx
│
├── middleware/
│   ├── auth.ts
│   ├── permission.ts
│   ├── guest.ts
│   └── index.ts
│
├── lib/
│   ├── axios.ts
│   ├── auth.ts
│   ├── jwt.ts
│   ├── query-client.ts
│   ├── env.ts
│   ├── storage.ts
│   └── constants.ts
│
├── utils/
│   ├── formatter.ts
│   ├── currency.ts
│   ├── slug.ts
│   ├── validator.ts
│   ├── date.ts
│   ├── image.ts
│   └── file.ts
│
├── types/
│   ├── api.ts
│   ├── auth.ts
│   ├── user.ts
│   ├── role.ts
│   ├── permission.ts
│   ├── branch.ts
│   ├── brand.ts
│   ├── car-model.ts
│   ├── product.ts
│   ├── banner.ts
│   ├── company-profile.ts
│   ├── setting.ts
│   └── audit-log.ts
│
├── public/
│   ├── favicon.ico
│   ├── images/
│   ├── icons/
│   └── logo.svg
│
├── styles/
│   ├── globals.css
│   └── tailwind.css
│
├── .env.local
├── .env.development
├── .env.production
├── middleware.ts
├── next.config.ts
├── tsconfig.json
├── package.json
└── README.md
```

---

# Struktur Feature

Setiap feature memiliki struktur yang sama sehingga mudah dikembangkan dan dipelihara.

```text
features/
└── products/
    ├── api/
    │   ├── get-products.ts
    │   ├── get-product.ts
    │   ├── create-product.ts
    │   ├── update-product.ts
    │   ├── delete-product.ts
    │   └── upload-image.ts
    │
    ├── components/
    │   ├── product-table.tsx
    │   ├── product-form.tsx
    │   ├── product-card.tsx
    │   ├── product-gallery.tsx
    │   └── product-filter.tsx
    │
    ├── forms/
    │   └── product-form-schema.ts
    │
    ├── hooks/
    │   ├── use-products.ts
    │   ├── use-product.ts
    │   ├── use-create-product.ts
    │   ├── use-update-product.ts
    │   └── use-delete-product.ts
    │
    ├── services/
    │   └── product.service.ts
    │
    ├── types/
    │   └── product.ts
    │
    ├── utils/
    │   └── product-helper.ts
    │
    └── validation/
        └── product.schema.ts
```

---

# Layer Arsitektur

```text
Page
   │
   ▼
Feature
   │
   ▼
Hook
   │
   ▼
Service
   │
   ▼
Axios Client
   │
   ▼
REST API
```

---

# Penjelasan Folder

| Folder | Fungsi |
|----------|--------|
| `app` | Routing menggunakan App Router |
| `components` | Komponen UI yang dapat digunakan ulang |
| `features` | Seluruh logika berdasarkan domain/fitur |
| `hooks` | Custom React Hooks |
| `services` | Komunikasi ke REST API dan layanan eksternal |
| `providers` | React Context Provider (Auth, Query, Theme, Toast) |
| `middleware` | Middleware aplikasi (auth, guest, permission) |
| `lib` | Library internal dan konfigurasi aplikasi |
| `utils` | Helper dan fungsi utilitas |
| `types` | Definisi TypeScript interface/type |
| `public` | Asset statis |
| `styles` | File CSS global |

---

# Konvensi Penamaan

| Jenis | Format |
|--------|--------|
| Folder | `kebab-case` |
| File React | `kebab-case.tsx` |
| Hook | `use-*.ts` |
| Service | `*.service.ts` |
| API | `*.api.ts` atau file per operasi (`get-*.ts`, `create-*.ts`) |
| Validation | `*.schema.ts` |
| Type | `*.ts` |
| Environment | `.env.*` |

---

# Prinsip Arsitektur

- **Feature-Based Architecture** untuk memisahkan domain bisnis.
- **App Router** digunakan sebagai entry point halaman.
- **Shared Components** ditempatkan di `components/`.
- **Business Logic** berada di dalam masing-masing `features/`.
- **Service Layer** menangani komunikasi dengan REST API.
- **TanStack Query** digunakan untuk data fetching dan cache.
- **React Hook Form + Zod** digunakan untuk validasi form.
- **Middleware** mengatur autentikasi dan otorisasi.
- **TypeScript** digunakan secara ketat (`strict mode`) untuk meningkatkan keamanan tipe data.
- Struktur ini dirancang agar mudah dikembangkan menjadi sistem yang lebih besar, seperti marketplace atau ERP, tanpa perlu mengubah fondasi arsitektur aplikasi.
