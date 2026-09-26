# Security Policy — Creative Motion Studio

**Project Architect & Author:** Fahad Iqbal  
**Professional Focus:** Full-Stack Developer • Cybersecurity • AI Engineering • Creative Technology

Security is an integral pillar of modern web applications and creative tools. Even client-side and media composition software must treat untrusted user inputs, file uploads, media streams, and external AI integrations with rigorous defensive engineering.

---

## 1. Supported Versions

| Version | Supported          | Security Maintenance Status |
| ------- | ------------------ | --------------------------- |
| 1.0.x   | :white_check_mark: | Actively Maintained         |

---

## 2. Core Security Architecture & Safeguards

### A. Environment Variable & Secret Protection
- Secret credentials (`AI_API_KEY`, tokens, database strings) are exclusively stored in server-side runtime environments and `.env.local`.
- No client-facing bundles (`NEXT_PUBLIC_`) ever expose provider secrets.
- `.env` files with active keys are excluded via `.gitignore`. An illustrative `.env.example` is provided for configuration guidance.

### B. Input Validation & Strict Schema Enforcement
- All project payloads, layer configurations, and canvas settings undergo strict type and bound validation via `lib/security/validation.ts`.
- Width, height, duration, and coordinates are bounded to prevent denial-of-service (DoS) from abnormal raster memory allocations.
- String inputs (project names, layer text, custom colors) are stripped of HTML tags (`<`, `>`) to mitigate Cross-Site Scripting (XSS).
- Color values are verified against rigid regex patterns (Hex, RGB, RGBA, HSL) to block code execution via CSS injection.

### C. File Upload Security
- Image uploads undergo multi-stage verification in `lib/security/upload.ts`:
  1. **MIME-type whitelist:** Only `image/jpeg`, `image/png`, `image/webp`, `image/gif`, and `image/svg+xml` are accepted.
  2. **File size boundary:** Hard cap of 8 MB prevents memory exhaustion attacks.
  3. **SVG Sanitization:** Vector SVG content is inspected and stripped of `<script>` tags, inline event attributes (`onload`, `onerror`, `onclick`), and `javascript:` URIs prior to canvas ingestion.

### D. Server-Side AI Rate Limiting
- The `/api/ai/creative-direction` route implements in-memory IP rate limiting (20 requests per minute per IP) to guard against brute-force token exhaustion and DoS attacks.
- Model responses are parsed with structured schema validation before transmission back to the client.

### E. Client-Side Sandboxing & Data Isolation
- Local project persistence uses isolated browser storage keys with schema migration checks.
- Media export leverages native Canvas APIs without third-party binary dependencies or remote code execution risks.

---

## 3. Reporting a Vulnerability

If you discover a potential vulnerability or security flaw:
1. Please do **NOT** open a public GitHub issue.
2. Send an email with reproducible steps and proof-of-concept details to:
   **fahad.iqbal.dev@gmail.com** (or reach out via Fahad Iqbal's verified GitHub profile).
3. Acknowledgements will be issued within 48 hours, followed by an assessment and patch release.
