# VIROX Admin Dashboard — Preview Build

## Open the dashboard
- Open `admin.html` in the same browser as the storefront, or run the project with VS Code Live Server.
- From the storefront, use the ADMIN link in the header.
- Click **Add product**, complete the fields, and save.
- Edit or delete products from the catalogue table.
- Use **Export CSV** to export the current product list.

## Product fields
- Product name, unique product ID / SKU
- Selling price and compare-at price
- Category, product badge, fabric/GSM
- Main image URL and extra image URLs (comma-separated)
- Sizes, colours, description, stock quantity
- Featured toggle

New product data is stored in browser `localStorage` under `virox-products`. The storefront reads the same key, so products added in the admin preview will appear in the shop when both are opened on the same origin/browser. Product pages use the product ID in `product.html?id=SKU`.

## Important limitations — before publishing
This is a **front-end admin prototype**, not a secure production admin system:
- Data is stored only in that browser. It does not sync across devices or browsers and can be cleared by browser storage cleanup.
- There is no administrator authentication or role protection. Do not publish this admin page publicly as a live management tool.
- Image fields accept image URLs; this build does not upload files to cloud storage.
- Stock is recorded in the admin preview but is not yet reserved/decremented by checkout.
- Orders, payments and customers are not managed here.

## Recommended production upgrade
Connect Supabase:
1. Supabase Auth for administrator sign-in.
2. `products` and `product_images` tables for permanent catalogue data.
3. Supabase Storage for product photo uploads.
4. Row Level Security so only approved admin users can insert, update or delete products.
5. Public read access only for active products.
6. Server-side order, price and stock validation before enabling live Cashfree payments.

Never put a Supabase service-role key or Cashfree secret in browser JavaScript. Only use the Supabase anon/publishable key in the client with correct Row Level Security policies.
