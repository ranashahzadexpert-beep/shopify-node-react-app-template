# Custom Shopify Embedded App Boilerplate (Node.js & React) 🚀

A high-performance, production-ready Shopify App boilerplate architecture built using modern full-stack technologies. This repository demonstrates professional app integration handling, OAuth authentication flows, secure webhook processing, and GraphQL API communications.

---

## 🛠️ Tech Stack & Architecture

* **Backend:** Node.js, Express.js
* **Frontend:** React.js, Shopify Polaris UI (Design System)
* **API Communication:** GraphQL (Admin API) & REST
* **Authentication:** Shopify App Bridge with Session Tokens (OAuth 2.0)

---

## 🚀 Key Technical Architectures Contained

### 1. Secure Webhook Handler (`/server/middleware/webhooks.js`)
* Implements strict HMAC verification for all incoming Shopify webhooks (e.g., `app/uninstalled`, `orders/create`) to ensure maximum security compliance.

### 2. Embedded Authentication Flow (`/server/auth/`)
* Handles seamless user authentication using offline and online session tokens, eliminating layout flashes and redirection loops inside the Shopify Admin.

### 3. High-Speed GraphQL Client (`/server/utils/graphql-client.js`)
* Demonstrates optimized bulk mutations and data queries using the Shopify GraphQL Admin API, handling automated rate-limit retries (Leaky Bucket algorithm).

---

## 💻 Sample Endpoint Structure

```javascript
// Example of a Protected Shopify Admin Route
app.get("/api/products/count", verifySessionToken, async (req, res) => {
  const client = new shopify.api.clients.Graphql({ session: res.locals.shopify.session });
  
  const data = await client.query({
    data: `{
      productsCount
    }`,
  });
  
  res.status(200).send({ count: data.body.data.productsCount });
});
