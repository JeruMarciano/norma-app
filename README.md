# Norma

Norma is a free app for people who run audits and compliance work on ISO 27001, NIS2 (ACN requirements) and ISO 42001: consultants, auditors and internal compliance leads.

It runs on your computer, with no server and no internet connection. You choose where Norma keeps your projects: a folder in Documents, in Google Drive, or anywhere else.

This is a beta (v0.3.0-beta.1). It may contain mistakes: keep a recent backup (see [Backups](#backups)).

## Downloading Norma

Open the [Norma v0.3.0-beta.1 release page](https://github.com/JeruMarciano/norma-app/releases/tag/v0.3.0-beta.1) and download the file for your computer:

| Computer | File |
|---|---|
| Mac with an Apple chip (M1 or later) | `Norma-0.3.0-beta.1-mac-arm64.zip` |
| Windows (64-bit) | `Norma-0.3.0-beta.1-win-x64.zip` |

**Which Mac?** Open the Apple menu (the apple at the top left) → **About This Mac**: you need a «Chip» line with «Apple M…». Macs with an Intel processor are not supported.

Norma has no installer: the zip contains the app, ready to open.

## First launch on a Mac

1. Double-click the zip: `Norma.app` appears.
2. **Move `Norma.app` to the Applications folder before opening it.** If you open it from Downloads, macOS runs it from a temporary read-only copy.
3. Norma is not signed by Apple, so macOS blocks it the first time. To open it:
   - right-click `Norma.app` → **Open** → **Open**;
   - if macOS offers no «Open» button (the case from macOS 15 Sequoia), try to open it once, then go to **System Settings → Privacy & Security**, scroll down and choose **«Open Anyway»**.

You need to do this the first time you open each downloaded version. After that, that same version opens normally.

## First launch on Windows

1. Right-click the zip → **Extract All**.
2. Extract it into a folder in your own profile, for example `Documents\Norma app` or `%LOCALAPPDATA%\Programs\Norma`. Do **not** extract it to the root of `C:\` or to a shared folder: there, other accounts on the same PC could change the program's files. Do not extract it into the Norma folder where your projects go (see below).
3. Open `Norma.exe` in the extracted folder.
4. Norma is not signed by Microsoft, so Windows shows «Windows protected your PC» (SmartScreen). Choose **«More info»** → **«Run anyway»**.

On PCs managed by a company IT department, or with **Smart App Control** turned on, Windows may block Norma without offering «Run anyway». In that case you need IT's approval.

## The first screen

The first screen offers two ways in:

- **«Start from scratch»**: you create an account, then choose where the Norma folder goes.
- **«I already have a Norma folder»**: you point Norma to an existing Norma folder (on Google Drive, for example) and restore its backup with the password, or the recovery code, that was valid when that backup was made. Use this on a second computer, after reinstalling, or on a new computer.

## Account, password and recovery code

You create the only account of that copy of Norma: your name and a password.

- The password must be at least 8 characters long. There are no rules about capitals or symbols: a sentence with spaces is fine. Passwords that are too common or easy to guess (such as your name or a single repeated character) are refused, and so are passwords longer than 1024 characters.
- After several wrong attempts, Norma makes you wait longer and longer before the next one.

Right after that, Norma shows a **recovery code** made of 6 groups. Write it down and keep it somewhere safe, away from the computer. To continue you must type its last group.

- Until you type the last group, Norma shows a new code at every sign-in, and only the last one shown is valid. Once you confirm it, the code stays the same.
- If you forget your password, choose **«I forgot my password»** on the sign-in screen, enter the code and set a new password. The code stays valid.
- To change your password: account menu → **Change password**.

**Without your password and without your recovery code you cannot open Norma's backups.** Nobody can open them, not even Norma's author. The files in the Norma folder stay readable (see below).

Your session ends when you close Norma, when you choose **Sign out**, or when the computer goes to sleep: you then need your password again, and anything you had not saved is lost. Locking the screen does not sign you out of Norma, and Norma does not lock itself when you are idle: lock your computer when you step away.

## The Norma folder

Right after the account, Norma asks where to keep your projects: **Documents on this computer**, **Google Drive** (if Norma finds it on the computer), or **another folder** (an external disk, Dropbox, OneDrive). Norma creates a folder called `Norma` there:

```
Norma/
├─ Backup di Norma.normabackup   encrypted, rewritten when you close Norma
├─ <Project name>/
│  ├─ Documenti di Norma/        documents Norma produces («Update in folder»)
│  ├─ Caricati in Norma/         files you upload through Norma
│  └─ … your own files and folders, wherever you put them
```

- **The files in these folders are ordinary, unencrypted files.** Anyone who can open that folder, or that Google Drive, can read them.
- You can add files to a project's folder yourself: Norma lists them on the project's Documents page and you can link them to a control as evidence. Norma never renames, moves or deletes your own files.
- Norma writes only the project folders with their «Documenti di Norma» and «Caricati in Norma», the backup file, a small hidden file (`.norma-owner.json`) that says which computer has Norma open, and short-lived hidden temporary files while it copies.
- Deleting a project in Norma leaves its folder and every file in it where they are.
- To move the whole Norma folder somewhere else: account menu → **Backup** → **Norma folder** → **Change**. Norma copies everything, checks every file, and only then removes the old copy.
- If the Norma folder is not there when Norma starts (Google Drive not started yet, a disk unplugged), Norma says «I can't find the Norma folder» and creates nothing in its place: start Drive or connect the disk and choose **Try again**.

Users of v0.2.0: at the first launch of this version Norma asks where to create the Norma folder and moves your existing attachments into the project folders, as ordinary files. Make a backup with v0.2.0 before updating.

## Where everything else is

Norma's database (projects, answers, risks, notes, the list of files), your account's keys and Norma's logs stay in Norma's data folder on this computer, never in the Norma folder:

- Mac: `~/Library/Application Support/Norma`
- Windows: `%LOCALAPPDATA%\Norma`

Do not edit or delete files in it by hand.

## Backups

**Automatic backup in the Norma folder.** When you close Norma, sign out, or the computer goes to sleep, Norma writes `Backup di Norma.normabackup` into the Norma folder. It holds the database, encrypted; the files are not in it, because they are already beside it in the folder. It replaces the previous one only once the new one is complete. This backup is how a second computer, or a new one, picks up your work.

**Manual backup.** Account menu → **Backup** → **Create backup** saves a single `.normabackup` file wherever you choose. It holds the database and the files of the project folders, except files over 100 MB and files missing from the folder: Norma tells you how many it left out. It is encrypted.

- Limit of this version: a manual backup can be at most 4 GB or 65,535 files. Beyond that, Norma does not save it and tells you so.
- Keep a manual backup off the computer and off Google Drive (a USB stick, an external disk): if the Norma folder is lost or damaged, its automatic backup goes with it.
- The home page shows when you made your last manual backup («Last backup: …»).

**Restoring.** Account menu → **Backup** → **Restore from backup**, or «I already have a Norma folder» on the first screen.

- Restoring **replaces all the data** in that copy of Norma. Norma says so and asks you to confirm.
- To open a backup you need the password, or the recovery code, **that was valid when the backup was created**. If you have changed your password since, use the old one or the code. After a successful restore those are your password and code again.
- If the restore fails, Norma goes back to the data you had before and tells you so.
- Files from a backup go back to their place in the project folders. A file that is already there and identical is skipped; a different file with the same name is never overwritten: the copy from the backup gets « (ripristinato)» in its name.
- A backup created by a newer version of Norma is refused: update Norma first.
- **Only restore backups you created yourself.** A `.normabackup` file contains instructions for the database: restoring a backup prepared by someone else is the same as running a program they wrote on your computer.

## Two computers, one Norma folder

You can use the same Norma folder on Google Drive from two computers, **one at a time**. Each computer has its own database: the work of the two is never merged.

- Close Norma on one computer before opening it on the other, and **wait until Google Drive has finished syncing** (its icon in the menu bar on a Mac, in the taskbar on Windows) before you open Norma on the second one. If you don't, Norma on the second computer may not yet see that the first one is open, and the work of one of the two can be lost.
- If the folder holds newer work from the other computer, Norma says so and offers **«Take the work from the other computer»** (a restore of the folder's backup, with your password). Until you take it, this computer's backup does not go into the folder.
- If the other computer still has Norma open, Norma says so. **«Work on this computer»** takes the folder anyway: use it only when the other computer crashed or was left open, because the work done there after its last backup stays on that computer.
- Working on the same projects at the same time from two computers is not possible in this version.

## Updating Norma

Norma does not check for new versions by itself. New versions are published on the **Releases** page of this repository.

1. Make a manual backup.
2. Close Norma.
3. Download the new zip and replace the old app: on a Mac, the new `Norma.app` in place of the old one in Applications; on Windows, the new extracted folder in place of the old one.
4. Open Norma. Your data and your Norma folder stay where they are.

The new version is not signed either: the first time, open it as in «First launch» above.

Before updating the database, Norma makes a copy of it (`pgdata.pre-update` in the data folder). If the update fails, Norma goes back to that copy and explains what happened.

## Uninstalling and reinstalling

1. Close Norma.
2. Delete the app (`Norma.app` on a Mac, the extracted folder with `Norma.exe` on Windows).
3. Delete the data folder (see [Where everything else is](#where-everything-else-is)). Your projects in Norma go with it; the Norma folder and its files stay where they are.

To reinstall later, or on another computer: install Norma, choose **«I already have a Norma folder»** on the first screen, point to the Norma folder and restore its backup. Do this only after the last computer that used the folder has closed Norma and Google Drive has finished syncing.

To remove everything, also delete the Norma folder. **This deletes your project files too.**

Outside these folders Norma writes only, on a Mac, its preferences file (`~/Library/Preferences/com.github.jerumarciano.norma.plist`). The system keeps its own records about the downloaded app: on a Mac, Gatekeeper and quarantine; on Windows, the SmartScreen decision and the «downloaded from the internet» mark on the zip file.

## Security: what Norma protects and what it does not

- **Norma does not connect to the internet.** No update checks, no usage statistics, no data sent anywhere. Norma's internal services listen only on the computer itself (`127.0.0.1`), not on the network. If the Norma folder is on Google Drive, it is Google Drive, not Norma, that copies its files to Google.
- **The files in the Norma folder are not encrypted**: documents, uploads and your own files can be read by anyone with access to that folder or that Drive.
- **Backups are encrypted** (AES-256-GCM): the automatic one in the Norma folder and the manual ones. The key opens only with your password or your recovery code.
- **The database is not encrypted.** Projects, answers, risks and notes can be read by anyone who copies the data folder and opens it with other tools. Signing in stops people who open Norma, not people who copy the database files.
- **Full copies of the database.** After an update that changes the database, Norma keeps `pgdata.pre-update`, a full, unencrypted copy of the database as it was before. It stays until a later update replaces it: data you delete in Norma can therefore remain there until then. During a restore, the folders ending in `.before-restore` hold your previous data and are deleted as soon as the restore succeeds.
- **Outside what Norma can protect against:** a malicious program already running under your user account on the computer. Such a program can do anything you can do.
- **Other people's backups:** see above, only restore backups you created yourself.
- **Spell checker:** on a Mac, Norma uses the system's. On Windows it is turned off, because it would download dictionaries from the internet.

If the computer holds client data, protect access to the computer itself: an account with a password and disk encryption (FileVault on a Mac, BitLocker on Windows). If the Norma folder is on Google Drive, protect that Google account too.

## Content under review

- **NIS2 (ACN requirements):** the ISO 27001 mappings are under review. Norma says so on the page: do not use them with a client yet.

## Checking the downloaded file

Norma is not signed by Apple. The only way to check that the file you downloaded is the one that was published, and has not been altered, is to compare its SHA-256 fingerprint.

The fingerprint is on the release page and in the attached `SHA256SUMS` file.

- **Mac:** open Terminal, type `shasum -a 256 ` followed by the path of the zip (you can drag the file into the window), then press Return. For example:
  ```
  shasum -a 256 ~/Downloads/Norma-0.3.0-beta.1-mac-arm64.zip
  ```
- **Windows:** open PowerShell and type:
  ```
  Get-FileHash $HOME\Downloads\Norma-0.3.0-beta.1-win-x64.zip
  ```

The fingerprint must be the same as the one written next to the file's name in `SHA256SUMS`. If it differs, do not open the file and download it again.

## Licence

Norma is free for every professional and organisation, but it is not open source. Its use is governed by [LICENSE.txt](LICENSE.txt) (Italian: [LICENZA.txt](LICENZA.txt), which prevails). You may share the original, unmodified zip files; please prefer sharing the link to this Releases page, where each file can be checked against `SHA256SUMS`. The third-party components included in Norma stay under their own licences, listed in the `THIRD-PARTY-NOTICES.txt` file inside the app (on a Mac: `Norma.app/Contents/Resources/`; on Windows: the `resources` folder next to `Norma.exe`).
