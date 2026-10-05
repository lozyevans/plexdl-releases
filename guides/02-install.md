# Installing and upgrading

PlexDL is installed on the **PC that runs your Plex Media Server**. It runs there as a Windows service, so it
works whether or not anyone is signed in, and you use it from any browser on your network.

## Before you start

- 64-bit Windows 10, 11 or Server 2016 or newer, and an account with admin rights.
- Plex Media Server installed and running on the same PC (or another PC on your network: see **Plex on a
  different PC** below).
- Free space for downloads while they're converted (PlexDL warns you if a drive gets low).
- An NVIDIA, Intel or AMD graphics chip makes conversions much faster, but isn't required.

You don't need to install Node.js, ffmpeg or anything else: the installer brings what it needs, and PlexDL
downloads its own checked copy of ffmpeg on first start.

## Get the installer

Download the latest **PlexDL-Setup-x.y.z.exe** (and its `.sha256`) from the
[PlexDL releases page](https://github.com/lozyevans/plexdl-releases/releases/latest), under **Assets**.

If you build PlexDL yourself: `npm run package` writes the installer to `dist\installer`, and every run of the
code repository's **Release** workflow keeps one as a download for 30 days.

Copy it to the Plex server, for example to `C:\Users\Public\Downloads`.

## Install

1. On the Plex server, double-click **PlexDL-Setup-x.y.z.exe** and allow it to make changes.
   - If Windows says "Windows protected your PC", choose **More info → Run anyway**. The installer isn't
     signed yet; you can compare its SHA-256 (`Get-FileHash .\PlexDL-Setup-x.y.z.exe`) with the `.sha256` file.
2. Accept the licence and keep the suggested folder.
3. Choose the options:
   - **Let other devices on my home network open PlexDL**: leave this ticked to use PlexDL from a phone or
     another PC (it opens the port for your local network only, never the internet).
   - **Run PlexDL as its own limited Windows account**: more secure; see below.
4. Keep port **32500** unless something else already uses it.
5. **Checking this PC** lists anything to fix first. Red items block the install and say how to fix them;
   grey notes are fine.
6. The installer sets up the **PlexDL** service, checks it starts, and opens `http://localhost:32500`.

From another device, open `http://<plex-server-name>:32500` (or its IP address, e.g.
`http://192.168.1.10:32500`).

## First sign-in

1. **Sign in with Plex** using the account that **owns** this Plex server. Nobody else can sign in.
2. The setup wizard opens. It walks through your Plex and friends' servers, which libraries to compare,
   where films and TV go (and whether PlexDL can write there), the file format, download limits that are
   kind to friends, optional automation and notifications. Every step shows what's set now and can be
   skipped; what you choose is saved as you go, and **Skip setup** keeps the defaults. Run it again any
   time from **System → Run setup again**.
3. **Finish and open Compare** runs the first sync (if PlexDL hasn't synced yet) and opens Compare.

## Plex on a different PC

PlexDL works best on the Plex PC, but it can run on another PC on the same network. In short:

1. Install PlexDL on that PC. **Checking this PC** warns that Plex isn't there; that's fine.
2. On that PC, open `http://localhost:32500`. Under the sign-in button choose **Plex on another PC?** and enter
   the Plex server's address, e.g. `http://192.168.1.10:32400`. Plex shows its private IP and port under
   **Settings → Remote Access**. This can only be done on the PlexDL PC itself, before anyone signs in.
3. Sign in with the account that owns that Plex server. PlexDL checks that plex.tv lists the address you entered
   for your server; if not, sign-in says so and you can correct it.
4. In **Settings → Import into Plex**, map each Plex folder to how this PC reaches it (e.g. `H:\Media` →
   `\\plexpc\Media`). Each folder shows a ✓ when PlexDL finds a file where Plex says it is.

The PlexDL service also needs a Windows account that can change files in those shares: see
[Plex on a different PC](07-plex-on-another-pc.md) for sharing the folders, the account, and the network ports.

Later you can change the address under **Settings → Your Plex server**.

## Moving from a trial install on another PC

If you tried PlexDL on another PC first and want to keep its settings, follows and history:

1. On the old PC: **System → Backups → Back up now**, then copy the newest folder from
   `C:\ProgramData\PlexDL\backups` to the Plex server.
2. Stop PlexDL on the old PC (or uninstall it) so the two don't both download the same things.
3. On the Plex server, after installing, run this from an **elevated** PowerShell in the PlexDL folder
   (`C:\Program Files\PlexDL`). It stops PlexDL, moves the current data aside (nothing is deleted), copies the
   backup in and starts PlexDL:

   ```powershell
   .\scripts\restore-backup.ps1 -Backup "C:\Users\Public\Downloads\2026-10-03_1200"
   ```

4. In **Settings → Import into Plex**, remove any drive mappings you needed on the old PC (such as
   `H:\ → \\server\H$`): on the Plex server PlexDL reaches the folders directly.

## Just the settings: export and import

To copy only your settings to another PlexDL (or give a friend a starting point), use **Settings → Export and
import settings**. **Export settings** saves one file with your download, conversion, destination, schedule,
notification and Media Manager settings, followed shows and collections, and your Don't download list. Your
sign-in, tokens, passwords and webhooks are never in it.

On the other PC, **Import settings…** shows what each part would change ("Downloads at once: 2 → 3", "Follows 3
more shows") and brings in only the parts you tick. Followed shows and lists are added to, never removed.
**This PC's folders** (staging, backup and inbox folders, path mappings) starts unticked, because they're
usually different on another PC. Notification channels keep this PC's webhooks and passwords: one that needs a
secret this PC doesn't have, or whose server or account changes, stays off until you add it. Choices that name
something on the other PC's Plex (a library that isn't here, or "same film" match choices from a different
Plex server) are left as they are here, and the preview says so. Each part either comes in whole or not at all.

Unlike a backup, this doesn't move your history, queue or sign-in.

## Limited account (optional)

Ticking **Run PlexDL as its own limited Windows account** makes PlexDL run as a hidden account called
"PlexDL" that can only change its own data and your library folders. After your first sign-in, run
**Grant PlexDL access to media folders** from the Start menu once (Settings → Import into Plex tells you when
it's needed), and again after you add a library to Plex.

## Upgrading

Run the newer installer on the Plex server. It stops PlexDL, backs up the database, keeps a copy of the current
version, installs the new one and checks it starts. Your sign-in, settings, queue and history are kept. If the
new version doesn't start, the installer puts the previous version and database back.

PlexDL checks for new versions once a day and shows a banner when one is out (System → Updates). It never
installs anything by itself.

## Uninstalling

Use **Settings → Apps** (or Start menu → PlexDL → Uninstall). It removes the service and the firewall rule and
asks whether to delete your PlexDL data (the default is to keep it). It never touches your media or your
`PlexDL Backup` folders.

## Installing without the wizard

For a silent install: `PlexDL-Setup-x.y.z.exe /VERYSILENT /PORT=32500` (add `/TASKS="!firewall"` to skip the
firewall rule). If the PC isn't ready, it stops and writes the reason to its log. To uninstall silently and
remove the data: `unins000.exe /VERYSILENT /REMOVEDATA=1` in the PlexDL folder.
