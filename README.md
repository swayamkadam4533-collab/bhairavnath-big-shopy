# Bhairavnath Big Shopy — Firebase starter v2

This package contains a customer page (`index.html`) and an admin page (`admin.html`).

## Features in this starter
- Admin email/password sign-in
- Add products with name, optional price, optional image, hide/show and delete
- Customer product catalogue; price appears only when the admin entered one
- Customer order form (name, 10-digit phone, items and notes)
- Customer request form for products not listed
- Admin order list and status changes: Order Placed, Preparing Order, Ready for Pick-up, Completed, Cancelled
- Basic order-status lookup using a display Order ID

## Important limitations / safety
- This is a starter, not a deployed/fully verified store. Configure Firebase before using it.
- Do not put customer data in a public GitHub repository. Only website source files belong there.
- The current simple order-status lookup uses a public `orderCodes` collection to find an order by display ID. For production, do NOT deploy this as-is because it is not a secure identity check and order status lookup is not protected by phone OTP. Implement Firebase Phone Authentication or a trusted Cloud Function before taking real customer orders.
- Public visitors can submit order/product-request forms, so spam controls/rate limits should be added before production.
- Never publish Firebase service-account keys. Web app config is not a service-account secret, but Firestore/Storage Security Rules must be correctly deployed.
- Firestore and Storage rules below require you to replace `PASTE_ADMIN_UID_HERE` with your Admin user's Firebase Authentication UID.
- Firebase free-tier availability/quotas can change; some features may require billing setup depending on usage/region.

## Setup from mobile
1. Extract this ZIP on your phone.
2. In Firebase Console, open your project.
3. Go to Project settings (gear) > General > Your apps > Add app > Web (`</>`). Register the app and copy the web config values into `firebase-config.js`.
4. Firebase Console > Build > Authentication > Get started > Sign-in method > enable Email/Password.
5. Authentication > Users > Add user. Create your admin email/password, then open that user and copy the UID.
6. Firestore Database > Create database. Start in production mode.
7. Paste the contents of `firestore.rules` in Firestore Database > Rules after replacing `PASTE_ADMIN_UID_HERE` with your Admin UID, then Publish.
8. Storage > Get started; paste `storage.rules` after replacing the same UID and publish. If Storage asks for a billing plan, do not enable billing unless you understand the charges; you can use products without photos until storage is configured.
9. Upload `index.html`, `admin.html`, `style.css`, `app.js`, `admin.js`, and `firebase-config.js` to your GitHub repository root. Do not upload rule files or customer data to GitHub.
10. In GitHub repo Settings > Pages, choose Deploy from a branch, `main`, `/(root)`, Save.
11. Open the Pages website and `/admin.html` to sign in.

## Mobile upload notes
GitHub's mobile interface may allow uploading files one at a time. Ensure `firebase-config.js` values are correct before expecting data to load.

## Before real launch
Have someone technically experienced review security rules and implement secure customer order access using Firebase Phone Authentication / OTP or a trusted backend. Test with dummy data first.
