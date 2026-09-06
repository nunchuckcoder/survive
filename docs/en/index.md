---
title: Privacy Policy — SURVIVE
---

# Privacy Policy — SURVIVE

[Português](../) · [English](./) · [Support](../support/) · [Delete data](../delete-data/)

**Last updated:** 28 August 2026  
**Controller:** Osvaldo Cipriano (NunchuckCoder)  
**Contact:** [osvaldo@osvaldocipriano.dev](mailto:osvaldo@osvaldocipriano.dev)

This policy transparently explains how the **SURVIVE** Android app handles data on the device.

## 1. Controller and scope

SURVIVE is developed by Osvaldo Cipriano (NunchuckCoder). The app runs locally on the Android device, and the developer does not receive or maintain a database containing data entered in the app.

## 2. Data stored on the device

The app may store locally:

- the profile's first and last name and email address;
- a cryptographic password derivative, salt, algorithm and iteration count;
- household details, including name, avatar, age, sex used for calculations, weight, height and activity;
- pantry products, quantities, units, categories, purchase and expiry dates, nutritional information, notes and usage history;
- stored medicines, including the entered commercial name/strength, category, quantity, unit, purchase date, expiry date and notes; this may constitute health information;
- bags, assignments to household members, categories, items, priorities, weight and checklist state;
- theme, configured warning period and the state of notifications already shown.

This data is used exclusively to provide SURVIVE features on the device itself.

The **Medicines** area is only for tracking stock and expiry dates of stored medicines. It provides no medical or pharmaceutical advice, diagnosis or prescription, and creates no dosage reminders or instructions.

## 3. Password and local security

The password is not stored as plain text. A cryptographic derivative with a salt and iteration count is stored locally.

The password blocks access through the app interface, but the Room database **is not encrypted by the password**. The app uses Android private storage, disables automatic system backups and sends no credentials to a server.

## 4. Android notifications and permissions

If allowed, notifications warn about products and medicines nearing expiry. Subject to Android privacy settings, a food notification may show the product name on the lock screen. Medicine notifications are generic: they do not show the medicine name; that detail remains inside the authenticated app.

The app uses only:

- **Notifications:** optional permission to show expiry warnings;
- **Completed boot:** restores the daily check after restarting or updating the device.

SURVIVE does not request access to location, contacts, camera, microphone, SMS or general device storage.

## 5. Backups

Export happens only when the user chooses to create a copy through the Android file picker. The exported JSON file:

- excludes the password, its hash and salt;
- may include other profile, household, pantry, medicine, history and bag data;
- is not encrypted by the app.

The chosen location and any later sharing of the file remain under the user's control and responsibility. Because the backup may contain medicine information, it should be stored in a private location. Restore reads only the file explicitly selected by the user.

## 6. Internet, third parties and advertising

SURVIVE:

- has no Internet permission;
- uses no WebView, remote API or online account;
- contains no advertising or analytics;
- uses no SDK intended to collect data;
- does not sell, share or transmit data to the developer or third parties.

## 7. Retention and deletion

Data remains on the device until the user changes or deletes it.

**Profile → Delete my profile** removes the profile and associated data. All data can also be deleted through Android settings or by uninstalling the app.

Previously exported backup files are not controlled by the app and must be deleted separately from their saved location.

## 8. Children's data

SURVIVE is not directed at children. An adult may enter a minor household member's data locally to obtain planning estimates. This data does not leave the device and is not collected by the developer.

## 9. Policy changes

This policy may be updated when app features or applicable requirements change. The published version will always show its latest update date.

## 10. Contact

For questions about this policy or privacy in SURVIVE:

**Email:** [osvaldo@osvaldocipriano.dev](mailto:osvaldo@osvaldocipriano.dev)

---

SURVIVE is an independent family preparedness planning app and does not represent a public body, emergency service or medical organisation.
