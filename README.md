# Norma

Norma is a free app for people who run audits and compliance work on ISO 27001, NIS2 (ACN requirements) and ISO 42001: consultants, auditors and internal compliance leads.

It runs on your computer, with no server and no internet connection. Your data stays in Norma's data folder, on your computer.

This is a beta (v0.2.0). It may contain mistakes: keep a recent backup (see [Backup and restore](#backup-and-restore)).

## Downloading Norma

Open the [Norma v0.2.0 release page](https://github.com/JeruMarciano/norma-app/releases/tag/v0.2.0) and download the file for your computer:

| Computer | File |
|---|---|
| Mac with an Apple chip (M1 or later) | `Norma-0.2.0-mac-arm64.zip` |
| Windows (64-bit) | `Norma-0.2.0-win-x64.zip` |

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
2. Extract it into a folder in your own profile, for example `Documents\Norma` or `%LOCALAPPDATA%\Programs\Norma`. Do **not** extract it to the root of `C:\` or to a shared folder: there, other accounts on the same PC could change the program's files.
3. Open `Norma.exe` in the extracted folder.
4. Norma is not signed by Microsoft, so Windows shows «Windows protected your PC» (SmartScreen). Choose **«More info»** → **«Run anyway»**.

On PCs managed by a company IT department, or with **Smart App Control** turned on, Windows may block Norma without offering «Run anyway». In that case you need IT's approval.

## Account, password and recovery code

On first launch you create the only account of that copy of Norma: your name and a password.

- The password must be at least 8 characters long. There are no rules about capitals or symbols: a sentence with spaces is fine. Passwords that are too common or easy to guess (such as your name or a single repeated character) are refused, and so are passwords longer than 1024 characters.
- After several wrong attempts, Norma makes you wait longer and longer before the next one.

Right after that, Norma shows a **recovery code** made of 6 groups. Write it down and keep it somewhere safe, away from the computer. To continue you must type its last group.

- Until you type the last group, Norma shows a new code at every sign-in, and only the last one shown is valid. Once you confirm it, the code stays the same.
- If you forget your password, choose **«I forgot my password»** on the sign-in screen, enter the code and set a new password. The code stays valid.
- To change your password: account menu → **Change password**.

**Without your password and without your recovery code there is no way back into Norma, and your attachments are lost.** Nobody can recover them, not even Norma's author.

Your session ends when you close Norma or when the computer goes to sleep: you then need your password again, and anything you had not saved is lost. Locking the screen does not sign you out of Norma, and Norma does not lock itself when you are idle: lock your computer when you step away.

## Where your data is

- Mac: `~/Library/Application Support/Norma`
- Windows: `%LOCALAPPDATA%\Norma`

This folder holds the database, the encrypted attachments and Norma's logs. Do not edit or delete files in it by hand.

## Backup and restore

A backup is your only protection against a broken or stolen computer, or a mistake. Norma makes no copies anywhere else.

- Account menu → **Backup** → **Create backup**. Norma saves a single `.normabackup` file wherever you choose. It holds everything: database and attachments. It is encrypted.
- Limit of this version: a backup can be at most 4 GB or 65,535 files. Beyond that, Norma does not save the backup and tells you so.
- Keep the backup off the computer (a USB stick, an external disk).
- The home page shows when you made your last backup («Last backup: …»).

To restore: account menu → **Backup** → **Restore from backup**. On first launch on a new computer, the start screen also offers **«Restore from a backup»**: this is how you move Norma to another computer.

- Restoring **replaces all the data** in that copy of Norma. Norma says so and asks you to confirm.
- To open a backup you need the password, or the recovery code, **that was valid when the backup was created**. If you have changed your password since, use the old one or the code.
- If the restore fails, Norma goes back to the data you had before and tells you so.
- After a successful restore you sign in with the password (and the recovery code) that were valid when the backup was created: they replace the ones you had before.
- A backup created by a newer version of Norma is refused: update Norma first.
- **Only restore backups you created yourself.** A `.normabackup` file contains instructions for the database: restoring a backup prepared by someone else is the same as running a program they wrote on your computer.

## Updating Norma

Norma does not check for new versions by itself. New versions are published on the **Releases** page of this repository.

1. Make a backup.
2. Close Norma.
3. Download the new zip and replace the old app: on a Mac, the new `Norma.app` in place of the old one in Applications; on Windows, the new folder in place of the old one.
4. Open Norma. Your data stays where it is.

The new version is not signed either, just like the first one: the first time, open it as in «First launch» (on a Mac, first move the new `Norma.app` to Applications).

Before updating the database, Norma makes a copy of it (`pgdata.pre-update` in the data folder). If the update fails, Norma goes back to that copy and explains what happened.

## Uninstalling

1. Delete the app (`Norma.app` on a Mac, Norma's folder on Windows).
2. Delete the data folder (see [Where your data is](#where-your-data-is)). **This also deletes all your data**: make a backup first if you need it.

Outside the data folder, Norma writes only, on a Mac, its preferences file (`~/Library/Preferences/com.github.jerumarciano.norma.plist`). The system keeps its own records about the downloaded app: on a Mac, Gatekeeper and quarantine; on Windows, the SmartScreen decision and the «downloaded from the internet» mark on the zip file.

## Security: what Norma protects and what it does not

- **Norma does not connect to the internet.** No update checks, no usage statistics, no data sent anywhere. Norma's internal services listen only on the computer itself (`127.0.0.1`), not on the network.
- **Attachments are encrypted** (AES-256-GCM). The key opens only with your password or your recovery code.
- **The database is not encrypted.** Projects, answers, risks and notes can be read by anyone who copies the data folder and opens it with other tools. Signing in stops people who open Norma, not people who copy the database files.
- **Full copies of the database.** After an update that changes the database, Norma keeps `pgdata.pre-update`, a full, unencrypted copy of the database as it was before. It stays until a later update replaces it: data you delete in Norma can therefore remain there until then. During a restore, the folders ending in `.before-restore` hold your previous data and are deleted as soon as the restore succeeds.
- **Outside what Norma can protect against:** a malicious program already running under your user account on the computer. Such a program can do anything you can do.
- **Other people's backups:** see above, only restore backups you created yourself.
- **Spell checker:** on a Mac, Norma uses the system's. On Windows it is turned off, because it would download dictionaries from the internet.

If the computer holds client data, protect access to the computer itself: an account with a password and, if you can, disk encryption.

## Content under review

- **NIS2 (ACN requirements):** the ISO 27001 mappings and «What to ask to see» are under review. Norma says so on the page: do not use them with a client yet.

## Checking the downloaded files

Norma is not signed by Apple or Microsoft. The only way to check that the file you downloaded is the one that was published, and has not been altered, is to compare its SHA-256 fingerprint.

The fingerprints are on the release page and in the attached `SHA256SUMS` file.

- **Mac:** open Terminal, type `shasum -a 256 ` followed by the path of the zip (you can drag the file into the window), then press Return. For example:
  ```
  shasum -a 256 ~/Downloads/Norma-0.2.0-mac-arm64.zip
  ```
- **Windows:** open PowerShell and type:
  ```
  Get-FileHash $HOME\Downloads\Norma-0.2.0-win-x64.zip
  ```
  PowerShell prints the fingerprint in capitals: upper and lower case count the same.

The fingerprint must be the same as the one written next to the file's name in `SHA256SUMS`. If it differs, do not open the file and download it again.

## Licence

Norma is free for every professional and organisation. Its use is governed by [LICENSE.txt](LICENSE.txt) (Italian: [LICENZA.txt](LICENZA.txt), which prevails). You may share the original, unmodified zip files; please prefer sharing the link to this Releases page, where each file can be checked against `SHA256SUMS`. The third-party components included in Norma stay under their own licences, listed in the `THIRD-PARTY-NOTICES.txt` file inside the app (on a Mac: `Norma.app/Contents/Resources/`; on Windows: the `resources` folder next to `Norma.exe`).
