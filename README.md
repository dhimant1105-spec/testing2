# PF Statutory — Option A (Browser-only login)

This edition removes Supabase and Firebase and runs as a static GitHub Pages website.

## Start
1. Upload `index.html`, `styles.css`, and `app.js` to a GitHub repository.
2. Enable GitHub Pages for the repository.
3. Open the published site. On first visit, create the initial Super Admin email and password.
4. Sign in and use **My login** in the sidebar to change the login email or password.
5. Use **Companies & users** (Super Admin) to create local company accounts.

## Critical limitations — read before using
This is Option A: login and all application data are stored in the visitor's browser `localStorage`.
- It is NOT secure authentication. Anyone with browser/developer-tool access can inspect or alter local data; client-side login cannot protect statutory records.
- Data is not shared between devices, browsers, or different users. Each browser has its own separate copy.
- Clearing browser data can permanently erase the records. Export/backup is not implemented.
- The local company/user roles are convenience controls only and can be bypassed by a technically capable visitor.
- Do not enter real employee UANs, payroll information, or confidential statutory records into this edition.
- This is unsuitable for a production statutory website. Use a server-side authenticated backend (such as the Firebase edition) for real company data.

## Existing statutory disclaimer
The ECR text export is a draft adapter, not certified as the current EPFO upload format. Verify the official schema, field order, validations, rates, ceilings, eligibility and exceptions before statutory filing.


## Updated wage calculation rules
- Calculated monetary values are rounded to the nearest whole rupee.
- Employee master CSV captures `employee_code` and `eps_membership_status` (`Yes`/`No`); `pension_member` is also accepted as a legacy header.
- Wage CSV template includes `gross_wages` and `pf_wages`. Gross wages may be left as 0 if not supplied.
- EPS wages are set automatically to `min(PF wages, EPS wage ceiling)` for EPS members and 0 for non-members. The uploaded CSV does not supply EPS wages.
- MPF = PF wages × configured employer PF (MPF) rate.
- EPS = EPS wages × configured EPS rate for EPS members; otherwise 0.
- CPF = MPF − EPS for EPS members; the CPF rate is not applied to pension members. For non-members, CPF = PF wages × configured non-pension CPF rate (default 12%).
- EDLI = min(PF wages, configured EDLI wage cap) × EDLI rate. Admin Charges = min(PF wages, configured Admin wage cap) × Admin rate. Both caps and rates are configurable in Statutory Settings.

These calculation rules are implemented as requested from the supplied reference image. Confirm the applicable statutory rates, caps, rounding conventions and EPFO filing requirements before production use.
