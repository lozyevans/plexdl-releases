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
2. Follow the setup checklist: which friends' libraries to compare, which of your libraries films and TV go
   to, and download settings.
3. On the Dashboard press **Full sync** once.

## Plex on a different PC

PlexDL works best on the Plex PC, but it can run on another PC on the same network:

1. Install PlexDL on that PC. **Checking this PC** warns that Plex isn't there; that's fine.
2. On that PC, open `http://localhost:32500`. Under the sign-in button choose **Plex on another PC?** and enter
   the Plex server's address, e.g. `http://192.168.1.10:32400`. Plex shows its private IP and port under
   **Settings → Remote Access**. This can only be done on the PlexDL PC itself, before anyone signs in.
3. Sign in with the account that owns that Plex server. PlexDL checks that plex.tv lists the address you entered
   for your server; if not, sign-in says so and you can correct it.
4. In **Settings → Import into Plex**, map each Plex folder to how this PC reaches it (e.g. `H:\` →
   `\\plexserver\H$`). Each folder shows a ✓ when PlexDL finds a file where Plex says it is.

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
