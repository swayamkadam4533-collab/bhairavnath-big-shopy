# Bhairavnath big shopy — free Store Pickup website starter

This is a mobile-friendly grocery ordering website with:
- Marathi / Hindi / English interface
- Product catalog, category filter, search and cart
- Store pickup time selection
- Cash or UPI payment at the store (no payment gateway)
- Order submission and customer order lookup
- Admin login, product CRUD and order status updates

## Important before using it for real customers
This starter is not connected to a database until you complete the Firebase setup below. The storefront displays demo products until Firebase is configured; demo orders cannot be submitted. Do not publish it as production-ready before setting up Firebase and reviewing the security rules. Order statuses are managed in the Admin Panel. Customer-facing order tracking needs a secure order token or customer login; the phone lookup UI is only a placeholder and will not read orders under the secure default rules.

## 1. Create a free Firebase project
1. Open https://console.firebase.google.com/ and create a project named `bhairavnath-big-shopy`.
2. Add a Web App in Project settings and copy the Firebase configuration.
3. In Authentication → Sign-in method, enable **Email/Password**.
4. In Authentication → Users, add your admin email and a strong password.
5. In Firestore Database, create a database (choose a location close to your customers if available).
6. Replace `REPLACE_WITH_YOUR_ADMIN_EMAIL` in `firestore.rules` with the exact admin email.
7. Publish the Firestore rules.

## 2. Add your Firebase config
In both `index.html` and `admin.html`, find `const firebaseConfig =` (in admin it is `const firebaseConfig=`) and replace:
- `PASTE_API_KEY`
- `PASTE_PROJECT_ID`
- `PASTE_SENDER_ID`
- `PASTE_APP_ID`
with the values from Firebase Project settings → Your apps. Keep the quotes.

Firebase web config is not a secret, but the Firestore security rules are essential. Never put a service-account key in this website.

## 3. Deploy for free
### Option A: GitHub Pages
1. Create a GitHub repository.
2. Upload `index.html`, `admin.html`, and any other needed files from this folder.
3. In repository Settings → Pages, choose deploy from the main branch/root.
4. Your customer site will be at `https://YOUR-USERNAME.github.io/REPOSITORY/`.
5. Admin page: `https://YOUR-USERNAME.github.io/REPOSITORY/admin.html`.

### Option B: Cloudflare Pages
1. Create a Cloudflare account and open Workers & Pages.
2. Create a Pages project from your Git repository.
3. Use the repository root as the build output directory; no build command is needed.
4. Use the URL Cloudflare gives you.

## 4. Add products
1. Open `admin.html` on the deployed site.
2. Sign in with the Firebase admin user you created.
3. Add products with English, Marathi and Hindi names, category, price, stock, and emoji.
4. Customers can then place orders from the homepage.

## 5. How store pickup works
- Customer adds products to cart and submits their name, mobile, pickup slot and payment preference.
- Payment happens at your store in cash or UPI. No payment gateway is included.
- Admin changes order status to Preparing, Ready for Pickup, and Completed.
- Customer-facing order status tracking is not enabled by default because exposing orders by phone number is not secure. Add a secure tracking token/auth flow before enabling it.

## 6. Free-plan and cost notes
- GitHub Pages and Cloudflare Pages have free tiers; quotas and terms can change.
- Firebase has a no-cost Spark plan, but quotas and features vary by product. Monitor usage in the Firebase console.
- A custom domain such as `bhairavnathbigshopy.com` is usually paid; use the free provider subdomain to stay at ₹0.
- No SMS/WhatsApp notifications are included.
- Free hosting does not mean unlimited traffic or guaranteed uptime.

## 7. Security notes (please read)
- Firebase API config is meant to be included in frontend apps; access is controlled by Firebase Security Rules.
- Admin write access is limited to the email configured in `firestore.rules`.
- Order documents are readable only by the admin account. Do not loosen these rules to expose orders by phone number; use an order-specific random tracking token or customer authentication to add customer tracking safely.
- Test order placement, product editing, and status updates with a test customer before sharing the website publicly.
