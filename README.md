# 🖨️ Press Orders — Order Book

A lightweight, cloud-synced order management web app built for **Shri Printers**, a print shop based in Mubarakpur. Tracks print orders, customer details, payments, delivery status, and generates printable bills — all in real time via Firebase.

---

## ✨ Features

- **Real-time sync** — All orders are stored and synced via Firebase Firestore. Changes reflect instantly across all open tabs/devices.
- **Order management** — Create, edit, and delete orders with full customer and job details.
- **Smart status tracking** — Track delivery status (`Pending → In Progress → Ready → Delivered`) and payment status (`Unpaid / Partial / Paid`) independently.
- **Quick actions** — One-click buttons on each order card to advance delivery stage or mark as paid, without opening the full edit form.
- **Printable bills** — Generate a clean, printable receipt/bill for any order directly from the browser.
- **Filtering & search** — Search by customer name; filter by order type, delivery status, and payment status simultaneously.
- **Sidebar views** — Quickly jump to Pending, Ready to Deliver, or Unpaid orders; or browse by order type (Wedding Cards, Binding, Magazines, etc.).
- **Live stats dashboard** — Header and stat cards show total orders, in-progress count, outstanding unpaid amount, and orders ready to deliver.
- **Auto payment status** — Payment status is automatically calculated from total amount vs. advance paid (no manual override needed).
- **Input validation** — Customer name, phone number (10-digit Indian mobile), quantity, dates, and amounts are all validated before saving.

---

## 🗂️ Order Types Supported

| Icon | Type |
|------|------|
| 💍 | Wedding Cards |
| 🧾 | Receipt Books |
| 📚 | Binding |
| 🎓 | Certificates |
| 📊 | Report Cards |
| 📰 | Magazines |
| 📦 | Other |

---

## 🧾 Order Fields

| Field | Description |
|-------|-------------|
| Customer Name | Required. Must be a valid name (not numbers/symbols). |
| Phone Number | Optional. Must be a valid 10-digit Indian mobile number. |
| Order Type | Required. Select from predefined print types. |
| Quantity | Optional. Must be a positive whole number. |
| Description / Specs | Free text — paper type, size, colour, special notes. |
| Order Date | Date the order was received. |
| Due / Delivery Date | Must not be before the order date. |
| Total Amount (₹) | Full price of the job. |
| Advance Paid (₹) | Must not exceed total amount. |
| Delivery Status | Pending / In Progress / Ready / Delivered. |
| Notes | Any additional internal notes. |

> **Payment status is auto-calculated:** If advance ≥ total → Paid. If advance > 0 → Partial. Otherwise → Unpaid.

---

## 🗄️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML, CSS, JavaScript (ES Modules) |
| Fonts | [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) + [DM Sans](https://fonts.google.com/specimen/DM+Sans) via Google Fonts |
| Database | [Firebase Firestore](https://firebase.google.com/docs/firestore) (NoSQL, real-time) |
| Hosting | Any static file host (Firebase Hosting, Netlify, GitHub Pages, etc.) |
| Build tools | None — zero dependencies, no bundler required |

---

## 🚀 Getting Started

### Prerequisites
- A Firebase project with Firestore enabled.
- A modern web browser (Chrome, Firefox, Edge, Safari).

### Setup

1. **Clone or download** this repository.

2. **Configure Firebase** — Open `index.html` and locate the `firebaseConfig` object near the bottom of the file. Replace it with your own Firebase project credentials:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

3. **Enable Firestore** in your Firebase Console:
   - Go to **Build → Firestore Database**
   - Click **Create database** → Start in **test mode** (or configure rules as needed)

4. **Open the file** — Simply open `index.html` in a browser. No server or build step required.

> **Tip:** For production use, serve the file over HTTPS (e.g., via Firebase Hosting or Netlify) to avoid browser restrictions on ES module imports.

---

## 🔐 Firebase Security Rules (Recommended for Production)

The default test-mode rules allow open access. For a real deployment, restrict access:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /orders/{orderId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Add Firebase Authentication if you want login-protected access.

---

## 🖨️ Printing Bills

1. Open any order → click **🖨️ Print Bill**
2. A formatted bill is shown with shop name, customer details, amounts, and status.
3. Click **🖨️ Print** to open the browser print dialog.
4. Sidebar, header, and toolbar are automatically hidden in print mode via CSS `@media print`.

---

## 📁 File Structure

```
press-orders/
└── index.html        # Entire app — single self-contained file
```

This is intentionally a single-file app for simplicity and portability.

---

## 🛣️ Possible Future Enhancements

- [ ] Firebase Authentication (login screen for staff)
- [ ] WhatsApp / SMS notification on order ready
- [ ] Export orders to Excel / CSV
- [ ] Monthly revenue reports and charts
- [ ] Customer order history (link orders by phone number)
- [ ] Dark mode toggle
- [ ] Mobile-responsive layout improvements

---

## 🏪 About

Built for **Shri Printers**, New Market, Mubarakpur.  
Proprietor: Parveen Gupta | 📞 +91 93572 72837

---

## 📄 License

This project is for private/internal use. Not licensed for public redistribution.
