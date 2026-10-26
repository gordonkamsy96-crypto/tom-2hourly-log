# TOM Supervisor's 2-Hourly Process Report (Android)

Android tablet app version of the paper/Excel log sheet **NBPOL/PLS/12, Rev 1** (`SHIFT_SUPERVISOR_2_HOURLY_REPORT.xlsx`).

## What it does
- **Form mirrors the sheet**: same 10-column grid and sections (Reception, Sterilization, Threshing, Power Generation,
  Press & Digester, Clarification, Kernel Recovery, Boiler, KCP, Quality Check, Remarks & Verification).
- Date / Time Start / Time Stop use pickers; "In operation" boxes cycle Yes / No on tap; numbers use the numeric keypad.
- **Handwritten signatures** for Shift Supervisor and Verified By (finger/stylus).
- **Autosave** while typing, plus *Save draft*. Reports list shows drafts and submitted reports.
- **Submit report** asks for: *Save & export PDF* / *Save only* / *Cancel*.
  Submitting locks the sheet, except the **Verified By** name, signature and date, so the verifier can sign afterwards
  and re-export.
- **Export PDF** (also available from the top bar and from each report in the list) writes a one-page A4 copy of the
  sheet to the tablet at **`Documents/TOM_Reports/`**, visible in the Files / My Files app. Re-exporting the same report
  overwrites its earlier PDF. Remarks too long for their box continue on a second PDF page, never cut off.
- Works fully offline. No permissions needed.

## Build the APK
1. Install **Android Studio** (Koala 2024.1.1 or newer) - it brings the Android SDK and JDK 17.
2. *File > Open* this folder, wait for the Gradle sync to finish.
3. Plug in the tablet (USB debugging on) and press **Run**, or use
   *Build > Build Bundle(s) / APK(s) > Build APK(s)*. The installable file is
   `app/build/outputs/apk/debug/app-debug.apk`.
4. To install on other tablets: copy the APK across and open it (allow "Install unknown apps" for the Files app).

Command line (JDK 17 + Android SDK installed): `./gradlew assembleDebug`

Requires Android 8.0 (API 26) or newer.

## Where things are
| File | Purpose |
|---|---|
| `FormSpec.kt` | The whole sheet layout. Keys are the Excel cell refs (e.g. `C11`). Change labels/fields here. |
| `FormUi.kt` | On-screen form (draws any `FormSpec`). |
| `PdfExporter.kt` | PDF page layout and saving to `Documents/TOM_Reports`. |
| `Signature.kt` | Signature pad. |
| `Report.kt` | Report model and on-device storage (JSON files in app storage). |
| `Screens.kt` | Reports list, form screen, submit / export dialogs. |
