# Job Application Autofill

A Chrome extension (Manifest V3) that fills the common fields on job application forms from a profile you save once, then moves through multi-step applications by clicking **Next / Continue** for you. It **stops before the final Submit** so you always review and submit yourself.

Everything stays in your browser. Your profile, resume and cover letter are stored in Chrome's local storage and are never sent anywhere.

## Features

- Fills name, email, phone (with country code), address, links, current company, title, experience, CTC, notice period, education and more
- Answers common screening questions (work authorization, sponsorship, relocation, gender, veteran and disability status)
- Uploads your resume (to "Resume" and "CV" boxes) and cover letter (to "Cover letter" boxes)
- Handles native selects, type-ahead comboboxes, Workday-style dropdowns and multi-select search boxes
- Auto-clicks Next / Continue / "Save and Continue" and waits for the next step, up to 12 steps
- Pauses and highlights required fields it could not fill, or fields the site rejected
- Custom answers: `keyword => answer` rules that take priority over the built-in rules
- "Clear all saved data" button on the profile page

## Install

1. Clone or download this repository.
2. Open `chrome://extensions` and turn on **Developer mode**.
3. Click **Load unpacked** and select this folder (the one containing `manifest.json`).
4. Pin the extension from the puzzle-piece menu.

## Set up your profile

1. Click the extension icon, then **Edit my profile**.
2. Fill in your details, upload your resume and optional cover letter, and click **Save profile**.
3. Review the screening answers (work authorization, sponsorship, etc.) so they match your situation.

## Use

1. Open a job application page (sign in first if the site requires it).
2. Click the blue **⚡ Autofill** button at the bottom right, press **Alt+Shift+F**, or use the popup: **Fill & continue all steps** or **Fill this step only**.
3. If it highlights fields in red, fix them and press Autofill again to continue.
4. On the last step, review everything and submit yourself. Solve any captcha manually.

Press **Esc** or click the button again (it shows "■ Stop") to stop a run.

## Settings

| Setting | Meaning |
| --- | --- |
| Overwrite existing values | Replace fields that already contain text (off by default) |
| Tick consent checkboxes | Tick terms / privacy / consent boxes (on by default) |
| Click Apply / Easy Apply | Open the form if it is not shown yet (on by default) |

## Supported sites and status

The engine is generic, with special handling for common applicant tracking systems.

| Site type | Status |
| --- | --- |
| Generic multi-step forms | Tested on a local mock form |
| Rippling | Tested on a copy of the real form structure |
| Workday | Dropdown and multi-select handling tested on a mock only; not tested on a signed-in real application |
| Greenhouse, Lever | Expected to work (mostly single-page forms); not tested on live pages |
| LinkedIn Easy Apply, Indeed, Naukri | Best effort; not tested on live pages. Naukri chat-style questions are not supported |

If it misses a field on a site, open an issue with the field's HTML (right-click the field, Inspect, copy element).

## Limitations

- It does not create accounts, sign in, or solve captchas.
- It never clicks the final Submit / Apply button.
- Fields inside shadow DOM or unusual custom widgets may not be detected.
- Some sites reset values on blur; re-run Autofill after fixing a rejected field.

## Project structure

```
manifest.json     Extension manifest (MV3)
background.js     Relays the shortcut and popup commands to the page
content.js        Field detection, filling and step navigation
options.html/js   Profile editor, resume / cover letter upload, clear data
popup.html/js     Quick actions
icons/            Extension icons
```

## Privacy

No analytics, no network requests, no remote code. Permissions used: `storage` (save your profile) and `activeTab` (run on the page you choose). The content script runs on web pages but only acts when you start it.

## Disclaimer

Review every application before submitting. Autofill can pick a wrong dropdown option or mis-read an unusual question. You are responsible for the accuracy of what you submit and for following each site's terms.
