
# 🔥 Firebase Setup & Admin Access Documentation

This document explains how to:

1. Obtain Firebase **client (public) configuration**
2. Obtain Firebase **Admin SDK credentials**
3. Securely store environment variables
4. Manually bootstrap the **first admin user**
5. Define the required Firestore collections and structure

---

## 1️⃣ Create a Firebase Project

1. Go to the Firebase Console  
   https://console.firebase.google.com
2. Click **Add Project**
3. Enter a project name (e.g. `gecian-hub`)
4. Disable Google Analytics (optional)
5. Click **Create Project**

---

## 2️⃣ Get Firebase Client (Public) Configuration

These values are used on the **frontend (Next.js)**.

### Steps

1. Firebase Console → **Project Settings**
2. Scroll to **Your Apps**
3. Click **Add App → Web**
4. Register the app
5. Copy the generated config

### Example

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "project-id.firebaseapp.com",
  projectId: "project-id",
  storageBucket: "project-id.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef"
};
````

---

## 3️⃣ Client Environment Variables

```env
NEXT_PUBLIC_FIREBASE_API_KEY=AIza...
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=project-id.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=project-id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=project-id.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=1234567890
NEXT_PUBLIC_FIREBASE_APP_ID=1:1234567890:web:abcdef
```

> 🔐 These values are **public by design** and safe to expose.

---

## 4️⃣ Enable Required Firebase Services

### Authentication

* Enable **Email / Password**
* Optional: Google Sign-In

### Firestore

* Create Firestore database
* Start in **Production Mode**
* Choose the correct region

---

## 5️⃣ Firebase Admin SDK (Server Side – SECRET)

The Admin SDK is required for:

* Admin management
* Secure Firestore writes
* Backend-only APIs

### Steps

1. Firebase Console → **Project Settings**
2. Open **Service Accounts**
3. Click **Generate new private key**
4. Download the JSON file

---

## 6️⃣ Storing Firebase Admin Credentials (Recommended)

### Option A: Individual Environment Variables (Best)

```env
FIREBASE_PROJECT_ID=project-id
FIREBASE_CLIENT_EMAIL=firebase-adminsdk@project-id.iam.gserviceaccount.com
FIREBASE_PRIVATE_KEY=-----BEGIN_PRIVATE_KEY-----\n...\n-----END_PRIVATE_KEY-----
```

> ✅ This avoids multiline parsing issues and is production-safe.

---

## 7️⃣ Firestore Admin Bootstrap (Critical)

Since no admin exists initially, the **first admin must be added manually**.

---

## 8️⃣ Firestore Collection Structure

### Correct Structure

```text
adminemail (collection)
└── auto-generated-doc-id
    ├── email: string
    ├── role: "admin" | "superadmin"
    ├── addedBy: string
    └── timestamp: timestamp
```

### Important Notes

* Use **Auto-ID** for documents
* Do **NOT** use email as document ID
* `role` must be controlled by backend only

---

## 9️⃣ Add First Admin Manually

### Steps

1. Firebase Console → Firestore Database
2. Click **Start Collection**
3. Collection ID: `adminemail`
4. Document ID: **Auto-ID**

### Fields

| Field     | Type      | Value                                                                 |
| --------- | --------- | --------------------------------------------------------------------- |
| email     | string    | [musthafalmukthar907@gmail.com](mailto:musthafalmukthar907@gmail.com) |
| role      | string    | admin                                                                 |
| addedBy   | string    | system                                                                |
| timestamp | timestamp | current time                                                          |

✅ This user is now the initial system admin.

---

## 10️⃣ Example Admin Document

```json
{
  "email": "psabhidram5600@gmail.com",
  "role": "admin",
  "addedBy": "system",
  "timestamp": "2025-09-04T11:51:19Z"
}
```

---

## 🔐 Recommended Firestore Security Rules

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /adminemail/{doc} {
      allow read: if request.auth != null;
      allow write: if false;
    }

    match /{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
