<!-- One module / one phase per PR. Keep PRs scoped to a requirement ID. -->

## Module / Phase
<!-- e.g. "Phase 0 — Login screen" / requirement IDs -->

- Module/Phase:
- Requirement ID(s):
- Target branch: <!-- dev1 for new work; dev2/test/prod for promotions -->

## Summary
<!-- What this PR does and why. -->

## Docs
- [ ] README / module docs added or updated for this change

## Checklist
- [ ] TypeScript — no new `any` without justification
- [ ] No authorization decisions made client-side (UI reflects server permissions)
- [ ] No tokens/secrets in localStorage or committed to code
- [ ] No `dangerouslySetInnerHTML` with user data
- [ ] Lint + type-check pass (ESLint, Prettier, tsc)
- [ ] `/security-review` run — no HIGH/CRITICAL findings
- [ ] Screenshots/recording attached for UI changes
