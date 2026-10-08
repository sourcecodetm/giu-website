# GIU Website Launch & Lead Collection Setup

## 1. Contact details already built into the website
- Email: gasisus@eszw.tech
- Phone / WhatsApp: +263 718 868 475
- Website: https://giu.eszw.tech

## 2. Important: how the spreadsheet works
The website is a static site. A normal `.xlsx` file inside the website package cannot be safely written to by visitors' browsers. Therefore the live version uses **Google Sheets + Google Apps Script** as the submission backend.

The package includes `GIU_Lead_Register_Template.xlsx` as a backup/template and `apps-script/Code.gs` as the live collector. Once the Google Sheet is created and the Apps Script web app is deployed, both the Join Pilot form and Investor/Partner form write into Google Sheets.

## 3. Create the live spreadsheet
1. Sign in to the Google account that should own GIU submissions.
2. Create a new Google Sheet named `GIU Website Lead Register`.
3. Open **Extensions → Apps Script**.
4. Open `apps-script/Code.gs` from this package and copy its full contents into the Apps Script editor.
5. Save the project.

The script automatically creates two tabs on the first submission:
- `Pilot Leads`
- `Investor Partner Leads`

## 4. Deploy the collector
In Apps Script:
1. Select **Deploy → New deployment**.
2. Select **Web app** as the deployment type.
3. Set **Execute as:** Me (the Google account that owns the Sheet).
4. Set **Who has access:** Anyone.
5. Deploy and complete Google's authorization prompts.
6. Copy the Web App URL. It normally ends in `/exec`.

Google recommends using a versioned deployment for public use rather than a head/test deployment. See the official Apps Script deployment documentation.

## 5. Connect the website to the spreadsheet
This launch package is already connected to the GIU Apps Script Web App endpoint:

`https://script.google.com/macros/s/AKfycbx5PC_u_vuMiXjsjkHYpIeuLQ6jy4JY_6P8ipzuc0fV8rBfWTVDSJjJ_iRPP8ere_0w/exec`

The endpoint is stored in `GIU_Website/config.js`. Do not put your Google Sheet ID or any Google credentials into the website. Only the public Web App URL belongs in `config.js`.
## 6. What happens when someone submits
### Join the Pilot
A submission is added to `Pilot Leads` with:
- Timestamp
- Name
- Phone / WhatsApp
- Email
- Area / Suburb
- Current Cooking Fuel
- Household Size
- Tank Size
- Interested Service
- Source

### Investor / Partner Enquiry
A submission is added to `Investor Partner Leads` with:
- Timestamp
- Name
- Organisation
- Email
- Phone / WhatsApp
- Interest type
- Message
- Source

The script also sends a notification email to `gasisus@eszw.tech` for each new submission.

## 7. How to access submissions
Open the Google Sheet `GIU Website Lead Register` using the Google account that owns it.

You can then:
- Filter pilot leads by suburb, household size, tank size or service.
- Filter investor/partner enquiries by interest type.
- Export/download the sheet as Excel or CSV.
- Share the Sheet with authorised GIU team members.

Do **not** make the spreadsheet publicly editable. Share it only with the GIU team members who need access.

## 8. Test before going live
1. Confirm the Apps Script deployment is **Execute as: Me** and **Who has access: Anyone**.
2. Open the website locally from `GIU_Website/index.html`, or from the published site.
3. Submit one test Pilot registration.
4. Confirm a new row appears in `Pilot Leads`.
5. Submit one Investor/Partner enquiry.
6. Confirm a new row appears in `Investor Partner Leads`.
7. Confirm notification emails arrive at `gasisus@eszw.tech`.
8. Remove only the test rows before launch.

### Recommended pilot test
- Name: GIU Test Customer
- Phone: +263 700 000 001
- Email: your email
- Area: Harare
- Current cooking fuel: LPG
- Household size: 3–4
- Tank size: 7 kg
- Interested in: Hot Swap

### Recommended investor test
- Name: GIU Test Investor
- Organisation: GIU Test Company
- Email: your email
- Phone: +263 700 000 002
- Interest: Strategic Partner
- Message: Website lead collection test.
## 9. Publish the website
The package contains a `CNAME` file containing:

`giu.eszw.tech`

When publishing with GitHub Pages, configure the repository's Pages custom domain as `giu.eszw.tech`, then create a DNS CNAME record for `giu` pointing to your GitHub Pages hostname. GitHub Pages supports custom subdomains and HTTPS.

Do not point `giu.eszw.tech` at the root `eszw.tech`; the CNAME should point directly to the GitHub Pages hostname.

After DNS is correct, enable **Enforce HTTPS** in GitHub Pages when the option becomes available.
