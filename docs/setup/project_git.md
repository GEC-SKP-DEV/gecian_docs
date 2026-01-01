
# 🚀 Gecian Hub – Complete Local Setup (Copy-Paste Ready)

This guide sets up **all Gecian Hub–related repositories**, installs dependencies, and prepares the environment for development.

---

## 📋 Prerequisites

Make sure you have:

* **Git**
* **Node.js (v18 or later)**
* **npm**

Verify:

```bash
git --version
node -v
npm -v
```

---

## 📁 Step 1: Create Workspace

```bash
mkdir gec_skp_dev
cd gec_skp_dev
```

---

## 📦 Step 2: Clone All Repositories

```bash
git clone https://github.com/GEC-SKP-DEV/gecian_hub.git
git clone https://github.com/GEC-SKP-DEV/gecian_project_collaboration.git
git clone https://github.com/GEC-SKP-DEV/Gec_Hostel.git
git clone https://github.com/GEC-SKP-DEV/gecian_project_archive.git
git clone https://github.com/GEC-SKP-DEV/student_app_backend.git
```

---

## ⚙️ Step 3: Install Dependencies (Inside Each Repo)

### 1️⃣ Gecian Hub (Frontend)

```bash
cd gecian_hub
npm install
cd ..
```

---

### 2️⃣ Project Collaboration

```bash
cd gecian_project_collaboration
npm install
cd ..
```

---

### 3️⃣ Gec Hostel

```bash
cd Gec_Hostel
npm install
cd ..
```

---

### 4️⃣ Project Archive

```bash
cd gecian_project_archive
npm install
cd ..
```

---

### 5️⃣ Student App Backend

```bash
cd student_app_backend
npm install
cd ..
```

---

## ▶️ Running the Applications

### Frontend

```bash
cd gecian_hub
npm run dev
```


Run other services as needed in separate terminals.

---



## 🧠 Notes for Contributors

* All repositories are **independent**
* Always run `npm install` after pulling updates
* Node version should be consistent across repos

---

## ✅ Setup Complete

At this point, your local directory should look like:

```
gec_skp_dev/
├── gecian_hub/
├── gecian_project_collaboration/
├── Gec_Hostel/
├── gecian_project_archive/
└── student_app_backend/
```

You are now ready to contribute 🎉


