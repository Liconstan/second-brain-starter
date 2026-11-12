# Contractor and 1099 review (US)

Treat annual filing rules as year-specific. Verify thresholds and classification with IRS and state sources before filing. Ramp Bill Pay supports 1099-NEC / 1099-MISC preparation and filing for supported customers; verify feature availability in the organization's account and jurisdiction.

1. Identify all contractor vendors, including those paid outside Ramp, and ensure W-9/W-8 **collection status** is known. Do not extract or display tax identification numbers in chat.
2. For each contractor, review total calendar-year payments, exact method (ACH/check vs card or qualifying payment network), tax classification, refunds/credits and whether funds were paid by an external provider. Avoid double-reporting amounts reportable by payment settlement entities on 1099-K.
3. Compare Ramp candidate list and exclusion reasons with ledger/vendor records. Ramp system suggestions or dollar threshold checks do not determine all legal eligibility.
4. For the applicable tax year, verify current federal and state form thresholds, deadlines, e-file requirements, and payer details against primary sources. As of Ramp's published 2026 guidance, its automated Bill Pay threshold for tax year 2026 is $2,000; reconfirm before the relevant filing season.
5. Produce `vendor token | aggregate payments | reportable candidate? | rationale | missing tax-doc status | exception | reviewer` table.
6. Obtain human sign-off before any filing, correction, recipient notice or IRS submission; don't file as agent.
7. If the organization previously had W-2 employees, verify payroll-tax account closure, outstanding zero-dollar returns, and any obligations left with a former payroll provider separately. Contractor-only current operations do not erase prior employee payroll responsibilities.

Never conclude that all contractor payments automatically require 1099s or that all outside-Ramp payments are included in Ramp calculations.
