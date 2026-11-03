# Security Policy

## Supported Versions

| Version | Supported | Security Maintenance |
| :--- | :--- | :--- |
| 1.0.x | Yes | Active vulnerability patches |
| < 1.0.0 | No | Deprecated |

---

## Vulnerability Disclosure Protocol

If you identify a security vulnerability, credential exposure, or authorization bypass in Learnza, please disclose it responsibly via email:

* **Security Contact**: goharrehmanfsd260@gmail.com
* **Repository Maintainer**: Gohar Rehman (@itsgoharrehman)
* **Response SLA**: Acknowledgment within 48 hours; status updates provided within 5 business days.

Please do not report vulnerabilities through public GitHub issues or discussions.

---

## Security Architecture and Invariants

### 1. Supabase Key Isolation
* **Public Anonymous Key**: The `SUPABASE_ANON_KEY` embedded in `js/config.js` is public by design. It provides strictly sandboxed read access governed by PostgreSQL Row-Level Security (RLS).
* **Service Role Key Invariant**: The Supabase `service_role` secret key must **NEVER** be committed to this repository or included in any client-facing script. Any PR or commit exposing a service role key will be rejected and the compromised key rotated immediately.

### 2. Row-Level Security (RLS)
* All relational tables (`books`, `categories`, `admin_audit_logs`) must have Row-Level Security explicitly enabled (`ENABLE ROW LEVEL SECURITY`).
* Unauthenticated or student users are restricted to `SELECT` operations on published materials.
* Modification operations (`INSERT`, `UPDATE`, `DELETE`) require authenticated JWT validation confirming administrative roles.

### 3. Edge Worker Streaming Security
* The Cloudflare Worker streaming proxy (`wrangler.jsonc`) enforces strict domain validation on origin URLs to prevent arbitrary open-proxy abuse.
* Response headers enforce binary attachment streaming (`Content-Disposition: attachment`) to prevent arbitrary script execution in client contexts.

### 4. Client-Side Input Sanitization
* All user queries and search parameters must be safely handled via parameterized Supabase queries or escaped using `textContent` rather than `innerHTML` to eliminate DOM-based Cross-Site Scripting (XSS).
