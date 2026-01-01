
# 🗄️ Database Setup (Neon) – One Database per Repository

This document explains:

1. How to access **Neon**
2. How to create a **separate database for each repo**
3. How to get the **DATABASE_URL**
4. How to link the database to **Next.js / Backend via `.env`**
5. Recommended naming & region strategy

---

## 📌 Important Rule (READ FIRST)

> **Each repository MUST use its own database**
> ❌ No shared databases
> ❌ No shared credentials
> ✅ One repo → one Neon database

This improves:

* Security
* Isolation
* Easier debugging
* Safe migrations

---

## 🧩 Repositories → Databases Mapping

| Repository                     | Database Name             |
| ------------------------------ | ------------------------- |
| `student_app_backend`          | `gecian_hub_backend`      |
| `gecian_events`                | `gecian_events`           |
| `gecian_project_archive`       | `gecian_project_showcase` |
| `gecian_project_collaboration` | `gecian_project_collab`   |
| `Gec_Hostel`                   | `nearbt_hostel`           |

---

## 1️⃣ Go to Neon Console

1. Open 👉 [https://console.neon.tech](https://console.neon.tech)
2. Sign in with GitHub / Email
3. You will land on the **Projects dashboard**

---

## 2️⃣ Create a New Neon Database (Per Repo)

Repeat these steps **for each repository**.

### Step-by-step

1. Click **New Project**
2. Fill details:

| Field                | Value                        |
| -------------------- | ---------------------------- |
| **Project name**     | e.g. `gecian_project_collab` |
| **Postgres version** | Default (recommended)        |
| **Region**           | Choose closest to users      |
| **Branch**           | `main`                       |

3. Click **Create Project**

⏳ Neon provisions the database automatically.

---

## 3️⃣ Choose Region (IMPORTANT)

### Recommended Regions

| Repo                     | Region                           |
| ------------------------ | -------------------------------- |
| India / Asia-facing apps | **AWS Asia Pacific (Singapore)** |
| Global / US-facing apps  | **AWS US East (N. Virginia)**    |

⚠️ **Do not mix regions randomly**

---

## 4️⃣ Get the Database Connection URL

After creation:

1. Open the Neon project
2. Go to **Dashboard → Connection Details**
3. Copy **Connection String**

It looks like this:

```text
postgresql://USERNAME:PASSWORD@HOST/DATABASE?sslmode=require
```

Example:

```text
postgresql://neondb_owner:password@ep-xyz.us-east-1.aws.neon.tech/neondb?sslmode=require
```

---

## 5️⃣ Link Database to Each Repo (`.env.local`)

### 🔹 Backend / Next.js Repo

Inside the repository root:

```bash
cp .env.example .env.local
```

Then edit `.env.local`:

```env
DATABASE_URL="postgresql://USERNAME:PASSWORD@HOST/DATABASE?sslmode=require"
```

---

## 6️⃣ Repo-wise `.env` Examples

### 🔸 `student_app_backend`

```env
DATABASE_URL="postgresql://.../gecian_hub_backend?sslmode=require"
```

---

### 🔸 `gecian_project_collaboration`

```env
DATABASE_URL="postgresql://.../gecian_project_collab?sslmode=require"
```

---

### 🔸 `gecian_project_archive`

```env
DATABASE_URL="postgresql://.../gecian_project_showcase?sslmode=require"
```

---

### 🔸 `Gec_Hostel`

```env
DATABASE_URL="postgresql://.../nearbt_hostel?sslmode=require"
```

---


## 8️⃣ Verify Connection Locally

Run:

```bash
npm run dev
```

If DB is connected correctly:

* No connection errors
* Migrations run successfully
* API routes work

---

## 9️⃣ Neon Dashboard – What You’ll See

For each database:

* **Name**
* **Region**
* **Created At**
* **Storage**
* **Branches**
* **Integrations**

Example:

```
gecian_project_collab
Region: AWS Asia Pacific (Singapore)
Branches: 2
Storage: ~31 MB
```

---

## 🔐 Security Rules (MANDATORY)

* ❌ Never commit `.env.local`
* ❌ Never reuse DATABASE_URL across repos
* ✅ Use `.env.example` for reference
* ✅ Rotate credentials if leaked

---
npx drizzle-kit push
also this to get teh scheme a there 