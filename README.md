# erp-frontend

Web client for the multi-tenant ERP (SaaS). React 18 + TypeScript + Vite, per
`TDR-001` (frozen stack). The mobile app uses Ionic React from a shared codebase.
See the BRD / `CLAUDE.md` for the binding architecture and security rules.

> ⚠️ The frontend never makes authorization decisions — it reflects them. Refresh
> tokens go in httpOnly + Secure + SameSite cookies, never localStorage. TypeScript
> everywhere; no `any` without justification. Read `CLAUDE.md` before contributing.

## Stack

| Layer | Technology |
|---|---|
| Framework | React 18 + TypeScript |
| Build tool | Vite |
| Mobile | Ionic React (single codebase, Android + iOS) |
| Lint/scan | ESLint (security plugin), Prettier, tsc, Semgrep |

## Getting started (local)

```bash
npm install
npm run dev
```

The dev server prints a local URL (default <http://localhost:5173>).

## Branching model

Code flows **up** through four long-lived environments. You never push directly to
`prod` or `test`; changes arrive there by promoting a green branch via Pull Request.

```
feature/module branch ──PR──▶ dev1 ──PR──▶ dev2 ──PR──▶ test ──PR──▶ prod
   (your work)              (integration)  (QA dev)   (staging)  (production)
```

| Branch | Purpose |
|---|---|
| `dev1` | Active development / integration. **Default branch** — open module & phase PRs here. |
| `dev2` | Second dev/integration stage. |
| `test` | QA / staging validation. |
| `prod` | Production. Release-only. |

## Per-module / per-phase workflow

Per `CLAUDE.md` §5: **one module or one phase at a time**, keyed to requirement IDs.

1. Branch off `dev1`: `git checkout dev1 && git pull && git checkout -b feature/<module-or-phase>`
2. Build the screen/feature; keep authorization server-driven (reflect, don't decide).
3. Add/Update docs for the module under `docs/` and update this README if needed.
4. Run lint/type-check + `/security-review`; fix findings.
5. Open a **Pull Request into `dev1`** using the PR template. Promotions up the chain
   (`dev1`→`dev2`→`test`→`prod`) are also PRs.

See `.github/pull_request_template.md` for the required checklist.

---

<details>
<summary>Vite + ESLint template notes (from the scaffold)</summary>

To enable type-aware lint rules for a production app, extend
`tseslint.configs.recommendedTypeChecked` (or `strictTypeChecked`) in
`eslint.config.js`, and consider `eslint-plugin-react-x` /
`eslint-plugin-react-dom`. See the [Vite React docs](https://vite.dev/).
</details>
