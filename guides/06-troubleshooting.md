# Troubleshooting

## Friends' servers

**"Offline" or "Never reached".** The server is switched off, or Plex's remote access isn't working for it.
Ask your friend to check Plex → Settings → Remote Access. PlexDL keeps trying, and still uses what it saw last
time. Offline servers are listed at the bottom of the Dashboard.

**"Relay (slow)".** PlexDL can only reach that server through Plex's relay, which Plex limits to a slow speed.
It works, but big files take a long time. Fixing your friend's remote access fixes this.

**"Downloads not permitted".** The owner hasn't allowed downloads for you. In Plex they edit their share with
you and turn on **Allow Downloads**. On Jellyfin they tick **Allow media downloading** for your user.

## Downloads and imports

**A download keeps failing.** The Queue shows the reason and a **Retry** button. Connection drops resume where
they stopped; PlexDL retries on its own a few times first.

**"Not enough space".** PlexDL won't start a download that wouldn't fit with room to spare. Free some space,
or change the reserve in Settings → Downloads. System → Storage shows when each drive will fill up.

**A title went to review.** Plex matched it to something else, or the file looked wrong. The Queue shows what
Plex chose with a link to it; fix the match in Plex and press **Mark as done**, or **Retry import**.

## Opening PlexDL

**PlexDL doesn't open.** Check the **PlexDL** service is running (Start → type "Services" → PlexDL → Start).
On the Plex server itself use `http://localhost:32500`.

**It opens on the server but not from other devices.** Use the server's name or IP address with port 32500.
The firewall option must have been ticked when installing (run the installer again to change it), and the
other device must be on the same home network.

**Port 32500 is in use.** Run the installer again and choose another port.

**"Windows protected your PC" when installing.** The installer isn't signed yet: **More info → Run anyway**.

## Getting help

- **Feedback** (top right, on every page) sends a problem or idea with a screenshot and diagnostics if you like.
  It goes straight to GitHub if a token is set in Settings → Feedback; otherwise it's saved as a zip to send.
- **System → Troubleshooting → Download diagnostics** gives one zip with the logs, health checks and settings,
  with every password and token removed.
- For a problem you can repeat, turn on **Detailed logging** first (it switches itself off after a day).
- Logs are in `C:\ProgramData\PlexDL\logs` (Start menu → PlexDL → PlexDL logs).

## Putting things back

- **History → Undo** takes an import back out (your previous copy comes back for upgrades).
- **Media Manager → Changes → Undo** reverses a tidy-up fix.
- PlexDL backs itself up every day. To restore one, from an elevated PowerShell in the PlexDL folder:
  `.\scripts\restore-backup.ps1 -Backup "C:\ProgramData\PlexDL\backups\<date>"`.
