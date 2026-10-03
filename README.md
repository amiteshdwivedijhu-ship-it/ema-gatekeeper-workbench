# Gatekeeper Workbench

Synthetic prototype of an AI-employee workbench, inspired by public Ema marketing pages (ema.ai). An AI employee drafts IT and finance work, pauses at the risky step for a human gate, and logs everything.

**Stack:** one self-contained `index.html` — no build, no dependencies, no backend. All data is synthetic ("Cobalt Freight", a fake 900-person logistics company; AI employees Ava, Finn, Hana).

## What it demonstrates

- Task queue (~25 synthetic tasks across IT, Finance, HR) with department/status filters and a "Needs you" count.
- Task view: the original request, the channel it came in on, and the AI employee's step-by-step plan with the source used for every step.
- Human gate: the plan stops at the risky step (grant admin access, pay over the auto-pay limit, change bank details) with what will happen, the policy reason, and a safer recommendation.
- Approve / Edit / Reject. Edit changes the action detail (e.g. 7-day access -> 1 day) before approval; the audit trail records the difference from the AI recommendation.
- Invoice variant: Finn matches PO and receipt, flags $18,900 over the $10,000 auto-pay limit, flags a possible duplicate of INV-2207, then stops for a finance approver.
- Audit trail per task and globally, with CSV export generated in the browser.
- Outcomes view: closed by AI alone vs. with a human gate, average close time, top gate reasons — baselines synthetic, this session updates them live.
- Session-persisted status via localStorage, with a Reset demo button.
- Empty state ("Needs you: 0") and an error state (simulated "Identity system did not respond" with retry).
- 375px phone layout: queue becomes cards, the plan stacks, and the gate becomes a bottom sheet with 44px buttons.

## Run locally

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Happy path (90 seconds)

1. Open "Admin access to Billing dashboard" (Slack, via Ava).
2. See the 6-step plan: role, manager, policy pass; step 4 (grant admin) is locked behind a human gate.
3. Approve with the recommended 7-day expiry.
4. Watch steps finish, the reply go out in Slack, and the task close as Done.
5. Check the audit trail and the outcomes view.

Not affiliated with Ema. No real systems, no real people, no real payments.
