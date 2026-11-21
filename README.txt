JRI STANDALONE HTTPS QR SCANNER

PURPOSE
This page runs the camera outside the Google Apps Script HTML Service iframe.
It does not access Google Sheets, store JRI data, or authorize users. It only
returns decoded QR text to the already-open JRI Sample Scanner tab using
postMessage with an exact return origin and per-launch channel value.

DEPLOYMENT
1. Deploy this folder as a static website on an HTTPS host (for example,
   GitHub Pages, Cloudflare Pages, Netlify, or an approved company web host).
2. Publish index.html at the site's root or a stable subfolder.
3. Copy the final HTTPS page URL.
4. In the Apps Script project's SampleScanner.html, set
   STANDALONE_SCANNER_URL to that exact HTTPS URL.
5. Save the Apps Script project and deploy a new web app version.
6. Open JRI > Sample Scanner, select the required stage, and click
   Open HTTPS Camera Scanner. Allow camera access for the standalone host.

IMPORTANT SECURITY / DATA FLOW
- Keep the authenticated JRI tab open. The standalone scanner must be opened
  from that tab; opening it directly is intentionally rejected.
- The parent JRI page checks the scanner's exact origin and launch channel.
- The parent page calls the existing Apps Script functions
  getTeamSamplingManifest() and recordSampleScan().
- Existing JRI authorization, Team QR validation, sample QR validation,
  scan-sequence enforcement, central tracking, and downstream Scan_Log writes
  remain in Apps Script and are not replaced by this static scanner.
- Do not add Apps Script credentials, spreadsheet IDs, API keys, or tokens to
  this static site.
- Serve only over HTTPS. Allow camera access for the standalone site's origin.

TEST CHECKLIST
1. Launch from an approved JRI account with SAMPLE_SCANNER / FG_USER /
   FG_CONTRACTOR_LEAD / HEAD / ADMIN access.
2. Scan a valid Team QR in FIELD TEAM CHECK-IN mode; verify the manifest and
   individual QR labels render in JRI.
3. Scan sample QR tags in order: LOWER CD, INTERMEDIATE, LABORATORY.
4. Verify out-of-sequence scans are rejected by JRI.
5. Verify unauthorized or unapproved users cannot access the JRI scanner page
   or its backend functions.
6. Verify QR PNG download and Print All Sample QR Labels still work.
