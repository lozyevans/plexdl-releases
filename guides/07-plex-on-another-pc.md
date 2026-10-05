# Plex on a different PC

PlexDL is happiest on the PC that runs Plex: it reaches your library folders directly and needs no extra set-up.
You can run it on another Windows PC on the same network instead, for example a faster PC for conversions or
one that's always on. This guide covers everything that changes.

## What you need

- Both PCs on the same home network, with fixed (reserved) IP addresses so they don't change.
- On the Plex PC: your library folders shared on the network (step 1).
- A Windows account that can change files in those shares, known to both PCs (step 2).
- On the PlexDL PC: free space for downloads while they're converted (the staging folder). Keep this on the
  PlexDL PC's own disk: only the finished file goes over the network.

## 1. Share the library folders on the Plex PC

On the Plex PC, share the folder **above** your library folders, so PlexDL's `PlexDL Backup` folder (next to
each library) is reachable too. For example, if Plex has `H:\Media\Movies` and `H:\Media\TV`, share `H:\Media`:

1. In File Explorer, right-click `H:\Media` → **Properties → Sharing → Advanced Sharing**.
2. Tick **Share this folder**, name it (e.g. `Media`), then **Permissions**: give the account from step 2
   **Change** and **Read**.
3. On the **Security** tab, give the same account **Modify**.
4. Make sure **File and Printer Sharing** is allowed in Windows Defender Firewall on the Plex PC (Control Panel
   → Windows Defender Firewall → Allow an app → File and Printer Sharing, Private networks).

Avoid the hidden admin shares (`H$`): Windows blocks them for local accounts coming over the network unless you
change a registry setting, and they expose the whole drive.

## 2. An account both PCs know

PlexDL runs as a Windows service, which can't use drives you map in Explorer. It reaches the shares as the
account the service runs as:

- **Home network (no domain):** create the same local user, with the same password, on both PCs (e.g.
  `plexmedia`): **Settings → Accounts → Other users → Add account → I don't have this person's sign-in
  information → Add a user without a Microsoft account**. Windows lets an account through when the name and
  password match on both sides. Set a password that doesn't expire.
- **Domain:** use a domain user (or a group managed service account) with the share permissions above.

Check it works before going on. On the PlexDL PC, open PowerShell as that user and try the share:

```powershell
runas /user:plexmedia powershell
# in the new window:
Test-Path \\plexpc\Media\Movies
New-Item \\plexpc\Media\plexdl-test.txt -ItemType File; Remove-Item \\plexpc\Media\plexdl-test.txt
```

Both should work without errors (`plexpc` is the Plex PC's name or IP address).

## 3. Install PlexDL on the other PC

Run **PlexDL-Setup-x.y.z.exe** on the PlexDL PC as in [Installing and upgrading](02-install.md), with two
differences:

- **Checking this PC** warns that Plex isn't installed there. That's expected.
- Leave **Run PlexDL as its own limited Windows account** unticked: step 4 sets the account instead.

## 4. Run the PlexDL service as that account

On the PlexDL PC:

1. Open **Services** (`services.msc`), double-click **PlexDL** → **Log On** → **This account**, enter
   `.\plexmedia` (or `DOMAIN\user`) and its password → **OK**. Windows gives it the "Log on as a service" right.
2. Let that account use PlexDL's data folder. In an **elevated** PowerShell:

   ```powershell
   icacls "C:\ProgramData\PlexDL" /grant "plexmedia:(OI)(CI)M" /T
   ```

   If you moved the staging folder (**Settings → Downloads**), grant the same on it.
3. Back in Services, **Restart** PlexDL, then open `http://localhost:32500`.

## 5. Point PlexDL at your Plex

1. On the PlexDL PC, open `http://localhost:32500`. Under the sign-in button choose **Plex on another PC?** and
   enter the Plex server's address, e.g. `http://192.168.1.10:32400` (Plex shows its private IP and port under
   **Settings → Remote Access**). This can only be done on the PlexDL PC itself, before anyone signs in.
2. **Sign in with Plex** with the account that owns that Plex server. PlexDL checks plex.tv lists that address
   for your server.
3. Later, change it under **Settings → Your Plex server**.

## 6. Map the library folders

Plex tells PlexDL where its folders are as the Plex PC sees them (`H:\Media\Movies`); PlexDL needs to know how
it reaches them. In **Settings → Import into Plex**, under **Library folders**:

1. Under **Folder mappings**, add one from the Plex path to the share, e.g. `H:\Media` → `\\plexpc\Media`
   (PlexDL offers a **Use …** button when it can guess one).
2. Each library should then show **OK** with its free space, and **✓ Found <file> where Plex has it**. "Can't
   reach" or "Can't write" means the mapping or the permissions are wrong; a red "may point at the wrong folder"
   means the mapping reaches a folder, but not the one Plex uses.

The same mappings are used by imports, Media Manager and the disk-space forecast. If a library's
`PlexDL Backup` folder can't sit next to it on the share, set a backup folder under **Advanced**.

## Network ports

| From | To | Port | What for |
| --- | --- | --- | --- |
| Your browser | PlexDL PC | 32500 (TCP) | Using PlexDL. The installer opens it for your local network only. |
| PlexDL PC | Plex PC | 32400 (TCP) | Talking to your Plex (scans, checks, Plex upkeep). |
| PlexDL PC | Plex PC | 445 (TCP) | The shared folders (File and Printer Sharing). |
| PlexDL PC | Internet | 443 (TCP) | plex.tv, friends' servers and downloads. |

## What works differently

- Imports copy the finished file over the network to a `.partial` file, check its size and then rename it, so
  an interrupted copy never leaves half a file in your library.
- **Pause conversions while Plex is converting for someone** still works: PlexDL asks your Plex.
- **Grant PlexDL access to media folders** (Start menu) is only for the limited account on the Plex PC; you
  don't need it here.
- The **Inbox** folder can be on either PC; give its path as the PlexDL PC reaches it.

## If something goes wrong

- **"Access is denied"** on a library folder: the service account can't change files there. Re-check steps 1, 2
  and 4 (share permission *and* folder security), then restart PlexDL.
- **Folder not reachable:** check the mapping and that `Test-Path` from step 2 works as that account.
- **Plex can't be reached:** check the address under **Settings → Your Plex server** and that the Plex PC's
  firewall lets port 32400 through.
- Everything else: [Troubleshooting](06-troubleshooting.md).
