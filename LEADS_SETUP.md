# Panduan Integrasi Borang (Google Sheets + Notifikasi Emel)

Gunakan kaedah percuma ini untuk menyimpan data pendaftaran terus ke Google Sheets anda, serta menghantar notifikasi emel segera kepada anda setiap kali ada pendaftaran baharu.

---

## Langkah 1: Sediakan Google Sheet
1. Buka [Google Sheets](https://sheets.google.com) dan cipta satu helaian (spreadsheet) kosong baharu.
2. Berikan nama helaian tersebut, contohnya: `Pendaftaran Desa Idaman`.
3. Pada baris pertama (Row 1), buat tajuk lajur seperti berikut:
   * **A1**: `Tarikh`
   * **B1**: `Nama Penuh`
   * **C1**: `Nombor Telefon`
   * **D1**: `Sektor Pekerjaan`
   * **E1**: `UTM Source` (Asal usul trafik - cth: fb, ig)
   * **F1**: `UTM Medium` (Medium iklan - cth: fbads)
   * **G1**: `UTM Campaign` (Nama kempen iklan Meta)
   * **H1**: `UTM Content` (Nama iklan/ad)
   * **I1**: `UTM Term` (Nama adset/sasaran)

---

## Langkah 2: Masukkan Google Apps Script
1. Pada menu bahagian atas Google Sheets, klik **Extensions** > **Apps Script**.
2. Padam semua kod lalai di dalam fail `Code.gs`, kemudian salin dan tampal kod di bawah:

```javascript
// Gantikan dengan emel anda untuk menerima notifikasi
const NOTIFICATION_EMAIL = "EMEL_ANDA@gmail.com";

function doPost(e) {
  try {
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    
    // Ambil data daripada borang HTML
    const name = e.parameter.name;
    const phone = "+60" + e.parameter.phone;
    const sector = e.parameter.sector;
    const utm_source = e.parameter.utm_source || "";
    const utm_medium = e.parameter.utm_medium || "";
    const utm_campaign = e.parameter.utm_campaign || "";
    const utm_content = e.parameter.utm_content || "";
    const utm_term = e.parameter.utm_term || "";
    const timestamp = new Date();
    
    // Masukkan baris baharu ke Google Sheet
    sheet.appendRow([
      timestamp, 
      name, 
      phone, 
      sector, 
      utm_source, 
      utm_medium, 
      utm_campaign, 
      utm_content, 
      utm_term
    ]);
    
    // Hantar notifikasi emel segera kepada anda
    MailApp.sendEmail({
      to: NOTIFICATION_EMAIL,
      subject: "🔥 Pendaftaran Baru Desa Idaman: " + name,
      htmlBody: `
        <h3>Pendaftaran Baru Diterima!</h3>
        <p><b>Nama:</b> ${name}</p>
        <p><b>Telefon:</b> <a href="https://wa.me/${phone.replace(/[^0-9]/g, '')}">${phone}</a></p>
        <p><b>Sektor Pekerjaan:</b> ${sector}</p>
        <p><b>Tarikh:</b> ${timestamp.toLocaleString()}</p>
        <br>
        <p><a href="https://wa.me/${phone.replace(/[^0-9]/g, '')}" style="background-color: #25D366; color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold;">Hubungi via WhatsApp</a></p>
      `
    });
    
    return ContentService.createTextOutput(JSON.stringify({ result: "success" }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({ result: "error", error: error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

3. Gantikan `"EMEL_ANDA@gmail.com"` pada baris ke-2 dengan alamat emel peribadi/jualan anda.
4. Klik butang **Save** (ikon disket) di atas.

---

## Langkah 3: Deploy Kod Sebagai Web App
1. Klik butang **Deploy** di sudut atas kanan > pilih **New deployment**.
2. Klik ikon gear di sebelah "Select type" > pilih **Web app**.
3. Sediakan konfigurasi berikut:
   * **Description**: `Borang Pendaftaran`
   * **Execute as**: `Me (emel anda)`
   * **Who has access**: `Anyone` *(Penting: pilih Anyone supaya borang di laman web boleh menghantar data).*
4. Klik **Deploy**.
5. Jika diminta, klik **Authorize Access**, pilih akaun Google anda, klik **Advanced** > **Go to Untitled project (unsafe)**, dan klik **Allow**.
6. Salin **Web app URL** yang diberikan (ia bermula dengan `https://script.google.com/...`).

---

## Langkah 4: Kemas Kini Laman Web Anda
1. Buka fail `index.html`.
2. Cari fungsi `handleFormSubmit(event)` di bahagian bawah fail (berhampiran talian JavaScript).
3. Gantikan nilai `'YOUR_GOOGLE_SCRIPT_WEB_APP_URL'` dengan URL Web App yang anda salin tadi:

```javascript
// Ganti dengan URL Google Script Web App anda
const scriptURL = 'TAMPAL_URL_DI_SINI';
```

4. Simpan fail, buat `git push`, dan Vercel akan mengemas kini laman web anda secara automatik!
