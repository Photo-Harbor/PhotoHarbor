# PhotoHarbor v1.0.0

A photo gallery and album manager for **Windows and Android**, created and maintained by a **solo developer**. Feedback and bug reports help shape future updates.

**App page and downloads:** https://github.com/Photo-Harbor/PhotoHarbor  
**Contact:** photoharbor.377@gmail.com

## What you can do

- Scan accessible folders/media and browse albums and photos.
- Search, sort, mark favourites and select multiple items.
- Rename album/display names, choose album covers and remove albums from the app without deleting originals.
- View photo details, zoom, use slideshows with timing/shuffle/repeat controls.
- Export originals, export albums as ZIPs and share media through supported system actions.
- Set wallpapers, move media to Trash, restore it and permanently delete items with confirmation.
- Find exact duplicate files and configure Trash cleanup.
- Choose light/dark/system appearance and interface language.
- Optionally download supported Instagram post/Reel media using gallery-dl.

Features depend on platform permissions and supported formats. Android videos open through a compatible external app. Removing an album from the app leaves originals alone; moving to Trash or permanently deleting can affect original files. Keep backups.

## Install on Windows

1. Open the app page above, then **Releases**.
2. Under **Assets**, download `PhotoHarbor-Setup-1.0.0-windows-x64.exe`.
3. Run the installer.
4. On **Select Destination Location**, click **Browse** to choose your installation folder, or keep the default:
   `%LOCALAPPDATA%\Programs\PhotoHarbor`.
5. Choose a folder your Windows account can write to. Protected folders may require additional permissions.
6. Keep **Install Instagram download support** selected if you want gallery-dl downloaded during setup. Uncheck it if you only want the local gallery.
7. Choose whether to create a desktop shortcut, then click **Install**.
8. Open PhotoHarbor, scan a photo folder and allow scanning to finish.

The installer places `gallery-dl.exe`, when selected, beside `photo_harbor.exe` in the chosen folder. PhotoHarbor detects it and saves its location automatically. An internet connection is needed for the optional download; setup lets you retry if it fails. The app does not silently download it on startup when it is missing.

Windows 10/11 on an x64-compatible system is the intended target. A compatible Microsoft Visual C++ x64 runtime may be needed. Keep required DLLs and the data folder with the app.

## Uninstall on Windows

1. Close PhotoHarbor.
2. Open **Windows Settings → Apps → Installed apps** (or **Apps & features** on Windows 10).
3. Find **PhotoHarbor**, select **Uninstall**, and follow the prompts.

Uninstall removes files registered by the installer. It does not intentionally delete your original photos, downloaded media or separate library/settings data. Back up anything important first. A gallery-dl file added manually after installation may remain in the installation folder.

## Install and uninstall on Android

1. Download the Android APK from **Releases → Assets**.
2. Open it and, if requested, allow **Install unknown apps** for your browser/file manager.
3. Install and open PhotoHarbor, grant photo/video access, then scan accessible media.
4. Android 11 or newer is required by the current build. Only permitted media can be shown.

To uninstall, long-press the PhotoHarbor icon and choose **Uninstall**, or use **Settings → Apps → PhotoHarbor → Uninstall**. Android removes private app data and saved in-app login sessions. Media exported/downloaded into shared folders can remain. Android manages the installation location; the custom folder chooser applies to Windows.

## Privacy: what stays on your device

PhotoHarbor's local gallery does **not upload your photos, files or personal information to the developer**. On Windows, it reads the PC name locally to label the computer in the interface; that name is not automatically sent to the developer.

To provide gallery features, PhotoHarbor also reads media you grant access to and stores catalogue records, file references, thumbnails, display names, favourites and preferences locally. It would therefore be inaccurate to say that it accesses only the PC name.

Optional online actions have their own network activity:

- Installing download support contacts its release host.
- Instagram login/downloads communicate with Instagram and its media servers, using the session you supply when required.
- Visiting the app page opens GitHub in your browser.
- Sharing or sending a support email sends only what you choose through the selected app/service.

Windows uses the selected cookies-file path; Android stores a selected session/cookies copy in private app storage. The gallery is not an encrypted vault or cloud backup service. Do not send cookies, passwords or private photo paths in support reports.

## Set up Instagram downloads on a Windows PC

### 1. Install or select gallery-dl

If you selected download support during installation, open **Settings → Downloads** and check that the engine location points to `gallery-dl.exe` in your installation folder.

If you skipped it:

1. Open **Settings → Downloads → Install download support**.
2. Confirm **Download** and wait for the result.
3. Alternatively, use **Open official download page**, obtain `gallery-dl.exe` from the official release, put it in the installation folder and select it using **Select gallery-dl.exe**.
4. Choose a **download destination folder** for saved photos/videos. This is separate from the application installation folder.

Official gallery-dl releases: https://codeberg.org/mikf/gallery-dl/releases

### 2. Prepare your Instagram login

1. Sign in to your own Instagram account in a supported browser.
2. Open the post/Reel you want to save and complete any login verification.
3. Close the browser completely before exporting cookies, including background windows if the cookies database is locked.
4. Open the PhotoHarbor installation folder in File Explorer. It should contain `gallery-dl.exe`.
5. Click File Explorer's address bar, type `powershell`, and press Enter. PowerShell now opens in that folder.

### 3. Export cookies with PowerShell

Replace `POST_ID` below with the post's code. This example uses **Opera**; use the browser where you signed in.

```powershell
.\gallery-dl.exe --cookies-from-browser opera/instagram.com --cookies-export "$env:USERPROFILE\instagram-cookies.txt" --simulate "https://www.instagram.com/p/POST_ID/"
```

For Firefox, replace `opera/instagram.com` with `firefox/instagram.com`. Chrome and Brave may fail to export because of browser encryption; changing the browser name alone does not overcome encryption restrictions.

The file is saved as `instagram-cookies.txt` in your Windows user folder. `--simulate` checks the post without downloading its media. Confirm that the export succeeded; an error or a file existing by itself does not prove that it contains a working Instagram session.

### 4. Select the exported file in PhotoHarbor

1. Open **Settings → Downloads → Instagram login (optional)**.
2. Click **Select cookies file**.
3. Open your Windows user folder and select `instagram-cookies.txt`.
4. Open **Downloads**, paste the post/Reel link, then click **Download and add to album**.
5. Check download history for the result. If a previous attempt failed, use **Retry**.

Cookies can grant access to your account. Keep this file private, never upload it to GitHub, and export a fresh session when it expires. Use PhotoHarbor's remove-cookies control when you no longer want the app to use it; the exported Windows file may also need deleting separately.

### Common errors

| Message/problem | What to do |
|---|---|
| `gallery-dl.exe` is not recognized | Open PowerShell in the folder containing the EXE and keep the `.\` prefix. |
| Permission denied reading browser cookies | Fully close the browser and retry. |
| DPAPI/decryption error | Update gallery-dl; if still unsupported, use your own session in another supported browser. |
| Redirect to login / session required | Check that sign-in/export succeeded, select the fresh cookies file and retry. |
| Private/unavailable post, rate limit or connection error | Check access/network, wait if rate limited and retry later. Cookies cannot guarantee access. |
| Cannot write to installation folder | Use a writable location or rerun setup to install download support. |

### Android Instagram login

Open **Settings → Downloads → Sign in to Instagram**. Complete sign-in and verification, then tap **Use session** when detected. Use **Sign out and remove session** to remove it. Importing a Netscape-format cookies file is also available. Browser/service restrictions can prevent login or downloading on some devices.

## Support

Use **Contact → Contact me** or email **photoharbor.377@gmail.com**. Include app version, Windows/Android version, what you expected and what happened. Add screenshots only after removing private information.

**Visit the app page** and **Share the app** both use:
https://github.com/Photo-Harbor/PhotoHarbor

PhotoHarbor is developed in a solo developer's free time. Thank you for feedback and patience while issues are investigated. Instagram availability and third-party behavior may change. Download only media you own or have permission to save.

## References

- gallery-dl command options: https://gdl-org.github.io/docs/options.html
- gallery-dl official releases: https://codeberg.org/mikf/gallery-dl/releases
