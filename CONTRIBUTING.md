# Contributing Guidelines

Thank you for contributing to Learnza. We appreciate community contributions that improve performance, expand catalog capabilities, enhance documentation, or resolve bugs.

---

## Code of Conduct

All contributors and participants are expected to adhere to our [Code of Conduct](CODE_OF_CONDUCT.md).

---

## Architectural Principles

Before writing code, please review our core architectural invariants:

1. **Zero Framework Bloat**: Learnza is deliberately built with vanilla ES6+ JavaScript, semantic HTML5, and standard CSS3. Do not add React, Vue, jQuery, or heavy UI libraries.
2. **Strict RLS Adherence**: Any database schema changes must reside in `db/database_setup.sql` and include strict Row-Level Security (RLS) policies.
3. **Safe DOM Manipulation**: Always use `textContent` or sanitized DOM creation methods. Avoid raw `innerHTML` insertions of user-supplied data to prevent DOM XSS.
4. **Credential Isolation**: Never commit Supabase service role keys, private Cloudflare tokens, or production database connection strings.

---

## Getting Started

1. Fork the repository:
   ```bash
   git clone https://github.com/<your-username>/learnza.git
   cd learnza
   ```

2. Create a focused branch:
   ```bash
   git checkout -b feature/category-filter-optimization
   # or
   git checkout -b fix/preview-loading-state
   ```

3. Install development tooling and run locally:
   ```bash
   npm install
   npm start
   ```

4. Verify changes locally across major browsers (Chrome, Firefox, Safari, Edge).

---

## Commit Guidelines

Use concise, imperative commit messages:

* `feat: add sort by publication year to catalog`
* `fix: handle network disconnect during pdf preview stream`
* `docs: clarify cloudflare worker deployment steps`
* `refactor: optimize dom rendering loop in main.js`

---

## Pull Request Process

1. Ensure all changes adhere to vanilla JavaScript conventions.
2. Verify that no secrets, credentials, or private keys are committed.
3. Test edge Worker modifications locally using `npm run dev`.
4. Open a Pull Request against the `main` branch and complete the pull request template checklist.
