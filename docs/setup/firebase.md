

# 🔥 Firebase Setup & Admin Access Documentation

This document explains how to:

1. Obtain Firebase **client (public) configuration**
2. Obtain Firebase **Admin SDK credentials**
3. Securely store environment variables
4. Manually bootstrap the **first admin user** in Firestore
5. Define the required Firestore collections and structure

---

## 1️⃣ Create a Firebase Project

1. Go to **Firebase Console**
   👉 [https://console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add Project**
3. Enter project name (e.g. `gecian-hub`)
4. Disable Google Analytics (optional)
5. Click **Create Project**

---

## 2️⃣ Get Firebase Client (Public) Configuration

These values are used on the **frontend (Next.js)**.

### Steps

1. Firebase Console → **Project Settings**
2. Scroll to **Your Apps**
3. Click **Add App → Web (</>)**
4. Register the app
5. Copy the generated config

Example:

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "project-id.firebaseapp.com",
  projectId: "project-id",
  storageBucket: "project-id.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef"
};
```

---

### ✅ Environment Variables (Client)

```env
NEXT_PUBLIC_FIREBASE_API_KEY=AIza...
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=project-id.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=project-id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=project-id.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=1234567890
NEXT_PUBLIC_FIREBASE_APP_ID=1:1234567890:web:abcdef
```

🔐 These are **public by design** and safe to expose.

---

## 3️⃣ Enable Required Firebase Services

### Authentication

* Enable **Email/Password**
* Optional: Google Sign-In

### Firestore

* Create Firestore database
* Start in **Production Mode**
* Choose correct region

---

## 4️⃣ Firebase Admin SDK (Server-Side – SECRET)

The **Admin SDK is REQUIRED** for:

* Admin management
* Firestore writes bypassing rules
* Secure backend APIs

### Steps

1. Firebase Console → **Project Settings**
2. Open **Service Accounts**
3. Click **Generate new private key**
4. Download the JSON file

Example:

```json
{
  "type": "service_account",
  "project_id": "project-id",
  "private_key": "-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n",
  "client_email": "firebase-adminsdk@project-id.iam.gserviceaccount.com"
}
```

---

## 5️⃣ Storing Firebase Admin Credentials 


### : FULL Admin SDK JSON (ONLY if needed)

```env
FIREBASE_ADMIN_SDK_KEY='{
  "type": "service_account",
  "project_id": "project-id",
  "private_key": "-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n",
  "client_email": "firebase-adminsdk@project-id.iam.gserviceaccount.com"
}'
```



---

## 6️⃣ Firestore Admin Bootstrap (CRITICAL)

Since no admin exists initially, **the first admin MUST be added manually** from the Firebase Console.

---

## 7️⃣ ✅ CORRECT Firestore Collection Structure

### ✔ YES — THIS STRUCTURE IS CORRECT

```text
adminemail (collection)
├── {autoDocId}
│   ├── email: string
│   ├── role: "admin" or "superadmin"
│   ├── addedBy: string
│   ├── timestamp: Timestamp
```

### 🔴 Important Notes

* **Document ID should be Auto-ID**
* Do **NOT** use email as document ID (causes problems later)
* `role` must be controlled by backend only

---

## 8️⃣ Manually Add First Admin (Bootstrap)

### Steps

1. Firebase Console → **Firestore Database**
2. Click **Start Collection**
3. Collection ID: `adminemail`
4. Document ID: **Auto-ID**

### Fields

| Field     | Type      | Value                                                                 |
| --------- | --------- | --------------------------------------------------------------------- |
| email     | string    | [musthafalmukthar907@gmail.com]| role      | string    | admin                                                                 |
| addedBy   | string    | emailid                                                                |
| timestamp | timestamp | current time                                                          |

✅ This user is now the **initial system admin**

---

## 9️⃣ Example Admin Document

```json
{
  "email": "psabhidram5600@gmail.com",
  "role": "admin",
  "addedBy": "psabhidram5000@gmail.com",
  "timestamp": "2025-09-04T11:51:19Z"
}
```

---

## 🔐 Security Rules (Recommended)

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /adminemail/{doc} {
      allow read: if request.auth != null;
      allow write: if false; // Admin SDK only
    }

    match /{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```
