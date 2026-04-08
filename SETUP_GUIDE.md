# ShopERP - Firebase Setup & Deployment Guide

## Step 1: Create Firebase Project (Free)

1. Go to https://console.firebase.google.com
2. Click **"Create a project"**
3. Name it: `shop-erp` (or any name)
4. Disable Google Analytics (optional) → Click **Create project**

---

## Step 2: Enable Realtime Database

1. In Firebase console, click **"Realtime Database"** (left menu)
2. Click **"Create Database"**
3. Choose region: **asia-south1 (Mumbai)** — closest to India ✓
4. Choose **"Start in test mode"** → Enable
5. Your database URL will look like:
   `https://shop-erp-default-rtdb.asia-south1.firebasedatabase.app`

---

## Step 3: Get Your Firebase Config

1. Click the **⚙ gear icon** → **Project Settings**
2. Scroll to **"Your apps"** section
3. Click **"</>"** (Web app icon)
4. Register app name: `ShopERP Web`
5. Copy the `firebaseConfig` object — it looks like:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "shop-erp.firebaseapp.com",
  databaseURL: "https://shop-erp-default-rtdb.asia-south1.firebasedatabase.app",
  projectId: "shop-erp",
  storageBucket: "shop-erp.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

---

## Step 4: Update index.html

Open `index.html` and find this section (around line 530):

```js
const firebaseConfig = {
  apiKey: "REPLACE_API_KEY",
  authDomain: "REPLACE_AUTH_DOMAIN",
  databaseURL: "REPLACE_DATABASE_URL",
  projectId: "REPLACE_PROJECT_ID",
  storageBucket: "REPLACE_STORAGE_BUCKET",
  messagingSenderId: "REPLACE_MESSAGING_SENDER_ID",
  appId: "REPLACE_APP_ID"
};
```

Replace ALL the `REPLACE_*` values with your actual Firebase config values.

---

## Step 5: Set Database Rules (Important for Security)

In Firebase Console → Realtime Database → **Rules** tab, paste:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

Click **Publish**. 
> Note: For production use, set up proper authentication rules later.

---

## Step 6: Deploy to Firebase Hosting (Free)

### Option A: Firebase Hosting (Recommended - Free forever)

1. Install Firebase CLI:
   ```
   npm install -g firebase-tools
   ```

2. Login:
   ```
   firebase login
   ```

3. In your project folder, run:
   ```
   firebase init hosting
   ```
   - Select your project
   - Public directory: `.` (current folder)
   - Single-page app: **Yes**
   - Don't overwrite index.html: **No**

4. Deploy:
   ```
   firebase deploy
   ```

5. Your app will be live at:
   `https://shop-erp.web.app` ✓

---

### Option B: Netlify Drop (Easiest - No CLI needed)

1. Go to https://app.netlify.com/drop
2. Drag and drop your `shopErp` folder
3. Done! You get a free URL like `https://amazing-shop-erp.netlify.app`
4. To get a custom URL, sign up and rename it

---

### Option C: GitHub Pages (Free)

1. Create a GitHub account at github.com
2. Create a new repository called `shop-erp`
3. Upload `index.html` and `manifest.json` to the repo
4. Go to Settings → Pages → Source: main branch
5. Live at: `https://yourusername.github.io/shop-erp`

---

## Step 7: Install as Mobile App (PWA)

### On Android (Chrome):
1. Open your app URL in Chrome
2. Tap the **3-dot menu** → "Add to Home screen"
3. App icon appears on home screen like a native app!

### On iPhone (Safari):
1. Open your app URL in Safari
2. Tap the **Share button** (box with arrow)
3. Tap **"Add to Home Screen"**
4. Tap Add — done!

---

## Default Login Credentials

| Role | Username | Password |
|------|----------|----------|
| Admin | admin | admin123 |
| Employee | emp1 | emp123 |
| Employee | emp2 | emp456 |

**Change these passwords after first login by editing the employee record!**

---

## Features Summary

- ✅ Real-time sync across all devices
- ✅ Works on mobile, tablet, desktop
- ✅ Cash Counter with Online + Cash breakdown
- ✅ Balance / Shortage calculation
- ✅ Inventory management with low stock alerts
- ✅ Sales tracking with payment type
- ✅ Expenditure tracking
- ✅ Employee attendance
- ✅ Salary management
- ✅ Offline indicator
- ✅ Installable as mobile app (PWA)

---

## Free Tier Limits (Firebase Spark Plan)

| Feature | Free Limit |
|---------|-----------|
| Realtime Database | 1 GB storage, 10 GB/month download |
| Hosting | 10 GB storage, 360 MB/day |
| Users | Unlimited |

This is **more than enough** for a single store. You won't hit these limits.
