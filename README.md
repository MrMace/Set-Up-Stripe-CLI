
# Stripe CLI Local Webhook Setup

### 1. Install Stripe CLI

### Windows (PowerShell — via Scoop)
```powershell
scoop install stripe
````

Or download the `.exe` directly:
https://github.com/stripe/stripe-cli/releases/latest


---

## 2. Login

```bash
stripe login
```

This will open a browser. Approve the request in your Stripe dashboard.

---

## 3. Start Your Local App

Make sure your app is running locally on a known port (e.g. `http://localhost:8080`).

---

## 4. Start the Listener

```bash
stripe listen --forward-to http://localhost:8080/stripe/webhook_abc123.php
```

Replace the path with your actual webhook endpoint.

---

## 5. Copy the Webhook Secret

The CLI will print something like:

```
> Ready! Your webhook signing secret is whsec_abc123... (^C to quit)
```

Copy that `whsec_...` value and set it in your local app config.

⚠️ **Important:**
Do NOT use the webhook secret from the Stripe dashboard — it will not work with the CLI.

---

## 6. Trigger a Test Event

In a second terminal:

```bash
stripe trigger payment_intent.succeeded
```

---

## 7. Check Your App Logs

If you see failures or non-200 responses in the CLI, check your app logs.

### Common Issues

* Wrong webhook path
* Incorrect `whsec` secret
* Database not connected locally
* Missing local config or credentials

