+++
date = '2026-03-08T23:05:06+07:00'
draft = false
title = 'TIL: The Mechanics of CSRF, Web Defense Strategies'
tags = ["csrf", "security", "web", "cookies"]
categories = ["Security"]
+++

Today I dove deep into **Cross-Site Request Forgery (CSRF)**. It’s a sneaky vulnerability because it doesn’t steal your data directly; instead, it "borrows" your active session to perform unauthorized actions on your behalf.

Here is a breakdown of how it works, why cookie settings matter, and how to defend against it in modern web apps.

## 1. The Classic Bank Example (How it Works)

Authentication is not the same as Authorization. Just because you are logged in doesn't mean every request coming from your browser was intentionally triggered by you.

1. **The Setup:** You log into your bank (`bank-abc.com`). Your browser stores a valid Session Cookie.
2. **The Trap:** You browse to a malicious site in another tab.
3. **The Trigger:** The malicious site contains hidden code (like an invisible form or an image tag) that triggers a request: `GET https://bank-abc.com/transfer?to=hacker&amount=1000000`.
4. **The Execution:** Your browser automatically attaches your active bank Cookie to this request. The bank sees a valid cookie and processes the transfer.

## 2. The Defense: Anti-CSRF Tokens in Node.js

The modern standard for preventing CSRF in Express/Node.js is using the **Double Submit Cookie** pattern via libraries like `csrf-csrf`.

The server generates a unique, random token and expects the client to send it back in a custom HTTP Header for any state-changing request (POST, PUT, DELETE).

```javascript
const express = require('express');
const cookieParser = require('cookie-parser');
const { doubleCsrf } = require("csrf-csrf");

const app = express();
app.use(cookieParser("your_secret_key")); 
app.use(express.json());

// Configure CSRF Protection
const { doubleCsrfProtection, generateToken } = doubleCsrf({
  getSecret: (req) => req.secret,
  cookieName: "x-csrf-token",
  cookieOptions: {
    httpOnly: true, // Crucial for XSS protection
    sameSite: "Lax",
    secure: process.env.NODE_ENV === "production", 
  },
  getTokenFromRequest: (req) => req.headers["x-csrf-token"],
});

// Endpoint to provide the token to the frontend
app.get("/get-token", (req, res) => {
  res.json({ csrfToken: generateToken(req, res) });
});

// Protect sensitive routes
app.post("/transfer-money", doubleCsrfProtection, (req, res) => {
  res.json({ message: "Transfer successful!" });
});

```

## 3. The `httpOnly` and `SameSite` Dilemma

I learned that setting `httpOnly: false` just so your frontend JavaScript can easily read the token from `document.cookie` is a dangerous anti-pattern.

If your site has a **Cross-Site Scripting (XSS)** vulnerability, hackers can inject JS to steal that token and bypass CSRF protections entirely.

While `SameSite: "Lax"` is a great defense mechanism, it has blind spots:

* It still allows cookies to be sent on top-level navigations (like clicking a link). If your API allows state changes via `GET` requests, you are still vulnerable.
* It can be bypassed if an attacker compromises a subdomain.

### Security Configurations Compared

| Configuration              | CSRF Protection | XSS (Cookie Theft) Protection | Verdict                    |
| -------------------------- | --------------- | ----------------------------- | -------------------------- |
| `httpOnly: true` + `Lax`   | **Strong**      | **Strong**                    | The industry standard.     |
| `httpOnly: false` + `Lax`  | **Moderate**    | **Poor**                      | Dangerous if XSS exists.   |
| `httpOnly: false` + `None` | **None**        | **Poor**                      | Leaves the door wide open. |

## 4. Real-World Application: Analyzing a Shopee API URL

Looking at a real-world API endpoint like `"https://seller.shopee.vn/webchat/api/coreapi/v1.2/mini/login?csrf_token=&source=pcmall&_api_source=pcmall"` reveals how production systems handle this:

* `csrf_token=`: The Anti-CSRF token. It's often left blank in the URL query if the system relies on checking the HTTP Headers instead (which is much safer than passing tokens via URLs where they can be logged or leaked).
* `source=pcmall`: Identifies the client platform (e.g., PC web interface vs. mobile app) so the server can route or format the response appropriately.
* `_api_source=pcmall`: An internal parameter usually used by API Gateways for traffic routing, analytics, and logging.
