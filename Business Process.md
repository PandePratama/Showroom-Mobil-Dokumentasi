# Business Process Documentation
# Website Landing Page Showroom Mobil Bekas

---

# Pendahuluan

Dokumen ini menjelaskan alur proses bisnis utama pada Website Landing Page Showroom Mobil Bekas menggunakan dua pendekatan visual:

1. **Flowchart** → menggambarkan alur proses secara sederhana.
2. **BPMN (Business Process Model and Notation)** → menggambarkan proses bisnis berdasarkan aktor (Admin, Sistem, Pengunjung).

Seluruh diagram menggunakan **Mermaid** sehingga dapat langsung digunakan pada GitHub, GitLab, Obsidian, atau editor Markdown yang mendukung Mermaid.

---

# 1. Login

## Flowchart

```mermaid
flowchart TD

A([Start])
B[Halaman Login]
C[Input Email & Password]
D{Validasi Form?}
E[Login ke API]
F{Credential Valid?}
G[Simpan JWT Token]
H[Redirect Dashboard]
I[Tampilkan Error]

A --> B
B --> C
C --> D
D -- Tidak --> I
D -- Ya --> E
E --> F
F -- Tidak --> I
F -- Ya --> G
G --> H
H --> J([End])
I --> C
```

## BPMN

```mermaid
flowchart LR

subgraph User
A(Start)
B[Input Login]
end

subgraph Backend
C[Validasi]
D{Valid?}
E[Generate JWT]
F[Return Token]
G[Return Error]
end

A --> B
B --> C
C --> D
D -- Ya --> E
E --> F
D -- Tidak --> G
```

---

# 2. Kelola User

## Flowchart

```mermaid
flowchart TD

A(Start)
B[Dashboard]
C[Pilih Menu User]
D[Daftar User]
E{Aksi}

E -->|Tambah| F[Input Data]
E -->|Edit| G[Update Data]
E -->|Delete| H[Soft Delete]
E -->|Reset Password| I[Generate Password Baru]

F --> J[Simpan]
G --> J
H --> J
I --> J

J --> K[Audit Log]
K --> L(End)
```

## BPMN

```mermaid
flowchart LR

subgraph Admin
A[Kelola User]
end

subgraph Sistem
B[Validasi]
C[Simpan Database]
D[Audit Log]
end

A --> B
B --> C
C --> D
```

---

# 3. Kelola Branch

## Flowchart

```mermaid
flowchart TD

A(Start)
B[Menu Branch]
C[Tambah/Edit Cabang]
D[Input Maps]
E[Validasi]
F[Simpan]
G[Clear Redis Cache]
H[Audit Log]
I(End)

A --> B --> C --> D --> E --> F --> G --> H --> I
```

## BPMN

```mermaid
flowchart LR

subgraph Admin
A[Kelola Branch]
end

subgraph API
B[Validasi]
C[Simpan Branch]
D[Redis Flush]
E[Audit]
end

A --> B --> C --> D --> E
```

---

# 4. Kelola Product

## Flowchart

```mermaid
flowchart TD

A(Start)

B[Menu Product]

C[Input Data Mobil]

D[Validasi]

E{Valid?}

F[Simpan Database]

G[Upload Gallery]

H[Publish]

I[Clear Cache]

J[Audit Log]

A-->B-->C-->D-->E

E--Tidak-->C

E--Ya-->F-->G-->H-->I-->J
```

## BPMN

```mermaid
flowchart LR

subgraph Admin
A[Input Product]
end

subgraph Backend
B[Validasi]
C[Simpan Product]
D[Generate Slug]
E[Redis Clear]
F[Audit]
end

A --> B --> C --> D --> E --> F
```

---

# 5. Upload Image

## Flowchart

```mermaid
flowchart TD

A(Start)

B[Pilih File]

C[Preview]

D[Upload Cloudflare R2]

E[Simpan URL]

F[Tentukan Primary Image]

G[Sort Order]

H(Selesai)

A-->B-->C-->D-->E-->F-->G-->H
```

## BPMN

```mermaid
flowchart LR

subgraph Admin
A[Pilih Gambar]
end

subgraph Backend
B[Upload R2]
C[Simpan Database]
end

A --> B --> C
```

---

# 6. Upload Video

## Flowchart

```mermaid
flowchart TD

A(Start)

B{Jenis Video}

B -->|Youtube| C[Input URL]

B -->|Upload| D[Upload File]

C --> E[Simpan]

D --> E

E --> F(End)
```

## BPMN

```mermaid
flowchart LR

subgraph Admin
A[Tambah Video]
end

subgraph Backend
B[Validasi]
C[Simpan]
end

A --> B --> C
```

---

# 7. Landing Page

## Flowchart

```mermaid
flowchart TD

A(Start)

B[Visitor]

C[Landing Page]

D[Banner]

E[Featured Product]

F[Company Profile]

G[Footer]

H(End)

A-->B-->C-->D-->E-->F-->G-->H
```

## BPMN

```mermaid
flowchart LR

subgraph Visitor
A[Buka Website]
end

subgraph Server
B[Redis Cache]
C[MySQL]
end

A --> B
B --> C
```

---

# 8. Search Product

## Flowchart

```mermaid
flowchart TD

A(Start)

B[Input Keyword]

C[Filter]

D[Search API]

E{Data Ada?}

F[Tampilkan Produk]

G[Data Tidak Ditemukan]

A-->B-->C-->D-->E

E--Ya-->F

E--Tidak-->G
```

## BPMN

```mermaid
flowchart LR

subgraph Visitor
A[Keyword]
end

subgraph Backend
B[Search]
C[Return JSON]
end

A --> B --> C
```

---

# 9. SEO Process

## Flowchart

```mermaid
flowchart TD

A(Start)

B[Publish Product]

C[Generate Slug]

D[Generate Meta]

E[Generate Schema]

F[Update Sitemap]

G[Clear Cache]

H(End)

A-->B-->C-->D-->E-->F-->G-->H
```

## BPMN

```mermaid
flowchart LR

subgraph Admin
A[Publish]
end

subgraph Backend
B[SEO Generator]
C[Sitemap]
D[Redis]
end

A --> B --> C --> D
```

---

# 10. Audit Log

## Flowchart

```mermaid
flowchart TD

A(Start)

B[User Action]

C[API]

D[Simpan Audit]

E[Database]

F(End)

A-->B-->C-->D-->E-->F
```

## BPMN

```mermaid
flowchart LR

subgraph User
A[Aksi]
end

subgraph Backend
B[Capture]
C[Audit Log]
D[Database]
end

A --> B --> C --> D
```

---

# 11. Dashboard

## Flowchart

```mermaid
flowchart TD

A(Start)

B[Login]

C[Dashboard]

D[Load Statistik]

E[Redis]

F{Cache Ada?}

G[Tampilkan]

H[Query Database]

A-->B-->C-->D-->E-->F

F--Ya-->G

F--Tidak-->H-->G
```

## BPMN

```mermaid
flowchart LR

subgraph Admin
A[Buka Dashboard]
end

subgraph Backend
B[Cek Redis]
C[Query Database]
D[Return Statistik]
end

A --> B
B -->|Cache Miss| C
B -->|Cache Hit| D
C --> D
```

---

# Ringkasan Business Process

| No | Proses | Aktor Utama |
|----|---------|-------------|
| 1 | Login | Admin |
| 2 | Kelola User | Super Admin |
| 3 | Kelola Branch | Super Admin |
| 4 | Kelola Product | Admin Cabang |
| 5 | Upload Image | Admin |
| 6 | Upload Video | Admin |
| 7 | Landing Page | Visitor |
| 8 | Search Product | Visitor |
| 9 | SEO Automation | Sistem |
| 10 | Audit Log | Sistem |
| 11 | Dashboard | Admin |
