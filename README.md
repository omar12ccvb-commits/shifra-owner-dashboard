# SHIFRA — Owner Console (Phase 2, part 1)

A single-file, no-build-step web dashboard for Omar and Youssef. It talks
**only** to your real backend — every number on screen is a live API call;
nothing is hardcoded or cached (spec #54).

## How to run it

1. Make sure the Phase-1 backend is running (`npm start` in `shifra-backend/`,
   see that project's README).
2. Open `index.html` in any browser — double-click it, or serve it with
   `npx serve .` for a nicer local URL.
3. Log in as `omar@shifra.internal` or `youssef@shifra.internal` with the
   password you set in the backend's `.env`.
4. If your backend isn't on `http://localhost:4000`, change the "عنوان
   السيرفر" field on the login screen before signing in.

## What's in it

- **نظرة عامة (Overview)** — the actionable-alerts view from spec #82:
  pending payment proofs, payouts ready to send, overdue projects,
  reconciliation mismatches. Click any alert to jump straight to it.
- **إثباتات الدفع (Payment Proofs)** — the review queue. Verify/reject
  buttons only appear for Youssef's account, matching the backend's own
  enforcement (spec #8) — Omar can see the queue but can't act on it, so the
  UI never promises something the API will then refuse.
- **المشاريع (Projects)** — filterable list, click through to a full
  drill-down (price history, payments, computed earnings) per spec #55.
- **الحسابات (Ledger)** — real account balances computed from ledger
  entries on every page load, plus a recent-entries feed.
- **المستحقات (Payouts)** — generate a cycle's payout batch, confirm
  (Youssef-only) with a real Vodafone Cash reference, or mark failed.
- **توزيع الأرباح (Profit Split)** — view the active split and its history;
  propose a new one (blocked client- and server-side unless it sums to 100%).
- **الدورة الأسبوعية (Weekly Cycle)** — current cycle, reconciliation
  (expected vs. actually paid), and the close-week action.
- **سجل التدقيق (Audit Log)** — every sensitive action, who did it, and when.

## Notes

- The session token lives in memory only, not `localStorage` — refreshing
  the page logs you out. For a console that can confirm real money
  movements, that's a deliberate trade-off, not an oversight.
- No design/verification was skipped for speed: every field this page
  renders was checked against a live response from the real API before
  being shipped (see the parent conversation for the exact checks run).

## Still not built (see the backend README's roadmap for full context)

Customer / Marketer / Editor apps, notifications delivery, device pairing,
and anything resembling deployment. This console is for the two Owner
accounts only.
