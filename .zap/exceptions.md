# ZAP Baseline — Documented Exceptions

## Exception: Rule 10038 — Content Security Policy (CSP) Header Not Set

**Status:** Approved exception (pending instructor sign-off)

**Rule ID:** 10038

**URL scope:** http://127.0.0.1:3000 (all paths) — applies only to the local
Juice Shop container used in this lab, not any production or staging system.

**Finding:** ZAP confirmed via baseline scan, and manual `curl` inspection of
HTTP response headers confirmed, that no `Content-Security-Policy` header is
returned by the application.

**Evidence:**
- Baseline scan run (enforcement mode, FAIL):
  https://github.com/Israel-Bright/juice-shop/actions/runs/34715586414/job/103612118577
- Manual curl verification: response headers inspected directly against
  http://127.0.0.1:3000, confirmed absence of `Content-Security-Policy`.

**Reason for exception:**
OWASP Juice Shop is an intentionally vulnerable training application
maintained upstream for security-education purposes. Modifying its
application code to add security headers is outside the scope of this
lab, which focuses on configuring and interpreting a ZAP baseline pipeline
rather than remediating the target application itself. Enforcing this rule
as a hard FAIL against an intentionally-vulnerable app is not a realistic or
useful gate for this environment.

**Owner:** Israel-Bright (student, repository owner)

**Approver:** Professor Dr. Ora Kenneth Melie (instructor) — pending
review/sign-off

**Compensating control:**
The finding remains visible in every scan run and is not silently suppressed;
it is tracked here explicitly with an expiration date. The underlying rule
stays enforced (FAIL) in `.zap/rules.tsv` so any *future* target scanned by
this same pipeline (e.g., a real internal app added to this workflow) would
still be blocked by this rule unless a similarly documented exception exists
for that scope.

**Expiration:** This exception applies only for the duration of this course
assignment (CPS-5981) and expires automatically at the end of the current
academic term. It should not be carried forward to any non-lab use of this
workflow.
