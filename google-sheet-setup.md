# Save Brain Drops waitlist signups to Google Sheets

The form already collects **Name, Email, City, Phone** and posts each signup to an
endpoint you own. Follow these steps once to wire it to a Google Sheet.

## 1. Create the sheet
1. Go to <https://sheets.new> and name it e.g. **Brain Drops Waitlist**.
2. In row 1, add these headers (exact, lowercase):

   `timestamp` | `name` | `email` | `city` | `phone` | `source`

## 2. Add the Apps Script
1. In the sheet: **Extensions → Apps Script**.
2. Delete any starter code and paste this:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
  var data = {};
  try { data = JSON.parse(e.postData.contents); } catch (err) {}
  sheet.appendRow([
    data.timestamp || new Date().toISOString(),
    data.name  || '',
    data.email || '',
    data.city  || '',
    data.phone || '',
    data.source || ''
  ]);
  return ContentService
    .createTextOutput(JSON.stringify({ ok: true }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. **Save** (disk icon).

## 3. Deploy as a Web App
1. **Deploy → New deployment**.
2. Gear icon → **Web app**.
3. Set **Execute as: Me**, **Who has access: Anyone**.
4. **Deploy**, authorize when prompted, and copy the **Web app URL**
   (looks like `https://script.google.com/macros/s/AKfy.../exec`).

## 4. Paste the URL into the design
- Open the **Tweaks** panel on the hero design and paste the URL into
  **sheetEndpoint**.

That's it. Every waitlist submission now appends a row to your sheet.

---

### Notes
- Submissions are also kept in the browser's `localStorage` under `bd-waitlist`
  as a backup, so nothing is lost if the network call fails.
- The request is sent with `mode: 'no-cors'` (the standard pattern for Apps
  Script), so the page can't read the response — the row still gets written.
- To change which fields are stored, edit both the headers and the `appendRow`
  order so they stay aligned.
