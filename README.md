# Frontend — Product Marketplace

Vue 3 + Element Plus frontend for a second-hand product marketplace. Features include browsing and searching products, publishing and managing your own listings, and an admin dashboard.

> The matching Flask backend lives on the [`backend`](https://github.com/houzhaohan/UNC-DATA703-project/tree/backend) branch.

This is a course project for **DATA 703** at the **University of North Carolina at Chapel Hill**, built by **Zhaohan Hou** and **Jiaxin Wang**.

## Tech Stack

| Component | Version |
|---|---|
| Node.js | ≥ 18 |
| Vue | ^3.5 |
| Vite | ^8.3 |
| Vue Router | ^4.6 |
| Pinia | ^4.0 |
| Element Plus | ^2.14 |
| Axios | ^1.20 |

## Directory Layout

```
frontend/
├── src/
│   ├── api/           # Axios instance + per-module API wrappers
│   ├── assets/        # Static assets (SVGs, images)
│   ├── router/        # Vue Router configuration
│   ├── stores/        # Pinia stores (auth)
│   ├── views/         # Page components
│   │   ├── ProductList.vue    # Product listing + search/filter
│   │   ├── ProductDetail.vue  # Product detail page
│   │   ├── ProductForm.vue    # Create / edit a product
│   │   ├── MyProducts.vue     # Current user's listings
│   │   ├── Login.vue          # Login
│   │   ├── Register.vue       # Registration
│   │   ├── Admin.vue          # Admin dashboard
│   │   └── HelpPage.vue       # Help / about page
│   ├── App.vue
│   ├── main.js
│   └── style.css
├── public/            # Unprocessed static files
├── dist/              # Build output (gitignored)
├── index.html
├── vite.config.js
└── package.json
```

## Prerequisites

```bash
node --version     # Make sure Node.js ≥ 18
npm install
```

## Development

```bash
npm run dev
```

Open `http://localhost:3032`.

During development Vite proxies `/api/*` to the remote backend (see `server.proxy` in `vite.config.js`). To target a local backend instead, update the proxy:

```js
proxy: {
  '/api': {
    target: 'http://localhost:3031',
    changeOrigin: true,
  },
},
```

## Production Build

```bash
npm run build
```

Output is written to `dist/`. Serve it with any static file server, for example:

```bash
npm run preview              # Preview the built app locally
# or
npx serve -s dist
```

## Routes

| Path | Page | Notes |
|---|---|---|
| `/` | ProductList | Browse and search products |
| `/products/:id` | ProductDetail | Product detail |
| `/products/new` | ProductForm | Publish a product (login required) |
| `/products/:id/edit` | ProductForm | Edit a product (owner only) |
| `/my-products` | MyProducts | Your listings (login required) |
| `/login` | Login | Sign in |
| `/register` | Register | Create an account |
| `/admin` | Admin | Admin dashboard (admin role required) |
| `/help` | HelpPage | Help & about |
