## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/146

**Issue title:** PII scrubber fails to redact parenthesized US phone numbers

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The PII scrubber currently recognizes dash-separated phone numbers like
555-123-4567 but misses the parenthesized area-code format (555) 123-4567,
which is one of the most common ways US phone numbers are written. Because
of that gap, the scrub() method leaves those numbers unredacted and
detect() reports no PII for them, so real personal data can slip through
the safety layer. The bug lives in the phone-number regex pattern in
pii_scrubber.py in the safety module. A successful fix extends that
pattern to also match the parenthesized format so both scrub() and
detect() handle it, which should turn the four related failing tests green
(test_us_phone_number_redaction, test_us_phone_formats, test_detect_phone_pii,
test_phone_at_start_of_text).

**Is this issue right for me? — checklist reasoning:**
This is a Tier 1 / good-first-issue bug scoped to a single file
(pii_scrubber.py). The issue includes clear reproduction steps and names
four existing failing tests, so success is unambiguous — I fix the regex
and watch red turn green. It does not require understanding the whole
architecture. The main scope risk is the regex itself: I need to add the
parenthesized format without breaking the existing dash format, which is
bounded and manageable.

**Branch name:** fix/146-pii-parenthesized-phone

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger
