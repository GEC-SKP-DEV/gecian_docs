

# 📄 Disclaimer & Legal Trigger 

## 1. Purpose of the Disclaimer

* Before using Gecian Hub, users must **acknowledge a disclaimer**.
* This ensures **legal awareness and consent** for terms of use, especially regarding:

  * Responsibility for posted content
  * Project limitations
  * Data handling practices

---

## 2. How the Disclaimer Works

* The disclaimer triggers **once per device/browser**.
* We use **IndexedDB** in the browser to remember if a user has accepted:

  * If IndexedDB is **present**, the disclaimer does not trigger again.
  * If IndexedDB is **cleared or missing** (e.g., new browser/device), the disclaimer will trigger again.

> ⚠️ This is **intentional** and recommended by legal counsel.

---

## 3. Legal Rationale

* The **lawyer advised** that a visible acknowledgment should be kept for each user session.
* IndexedDB provides a **lightweight, local-only solution** without storing personal data.
* This ensures:

  * **Compliance with legal advice**
  * **No personal data storage**
  * Users are **aware of their responsibilities**

---

## 4. Responsibility Statement

* Gecian Hub **does not store personal data**.
* The disclaimer only tracks acknowledgment locally for a device/browser.
* If a user clears IndexedDB or switches devices, the disclaimer will reappear.

> ⚠️ Future contributors or leads **must not bypass or remove this mechanism**, as it is a legal requirement.

---

## 5. Contributor Notes

* Contributors implementing new features should:

  * Respect the **disclaimer trigger**
  * Avoid storing personal information without legal approval
  * Consult the core lead if a feature requires tracking users

* The project **cannot be held liable** if a contributor bypasses this disclaimer or misuses user data.

---
