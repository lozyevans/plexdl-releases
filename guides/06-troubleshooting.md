# Troubleshooting

System shows a check for each part of PlexDL: amber works but is worth a look, red means something has
stopped. The **?** next to a check, or next to a problem in the Queue, opens its entry here.

## Friends' servers

**"Offline" or "Never reached".** The server is switched off, or Plex's remote access isn't working for it.
Ask your friend to check Plex → Settings → Remote Access. PlexDL keeps trying, and still uses what it saw last
time. Offline servers are listed at the bottom of the Dashboard.

**"Relay (slow)".** PlexDL can only reach that server through Plex's relay, which Plex limits to a slow speed.
It works, but big files take a long time. Fixing your friend's remote access fixes this.

**"Downloads not permitted".** The owner hasn't allowed downloads for you. In Plex they edit their share with
you and turn on **Allow Downloads**. On Jellyfin they tick **Allow media downloading** for your user.

## Your Plex and the library index

### plex.tv account

PlexDL signs in to Plex with your account to find your server and your friends' servers. **"Your Plex
sign-in has expired"**: press **Sign out** (top right) and sign in again. **"Can't reach plex.tv right now"**:
your internet connection or plex.tv is down; PlexDL carries on with what it already knows and tries again.

### Your Plex server

**"Not found yet"**: right after the first sign-in, give it a minute. **"… isn't answering"**: Plex Media
Server isn't running, or (when PlexDL is on another PC) its address has changed: check it in Settings → Your
Plex server. While your server is unreachable PlexDL can't add anything to Plex, but downloads carry on.

### Library index

PlexDL keeps its own list of what's on every server, refreshed by a full sync every night and quick syncs
during the day. **"Never synced"**: press **Full sync** on the Dashboard. Amber means the last sync was more
than two days ago: check the schedule in Settings → Schedule, and that PlexDL was running overnight.

## Folders and space

### Library folders

PlexDL must be able to write to every folder Plex uses for your libraries. **"PlexDL can't write to …"**: with
the limited account, run **Grant PlexDL access to media folders** from the Start menu, then **Check again** in
Settings → Import into Plex. When PlexDL is on another PC, the folder needs a mapping to a mapped drive or a
share, and perhaps a login for that PC (see [Plex on a different PC](07-plex-on-another-pc.md)). Amber with
"No Movie or TV libraries" means your Plex has none yet.

### Download folder

The staging folder where downloads wait to be converted. Red means its drive has less free space than PlexDL
keeps spare (Settings → Downloads → Keep free on staging drive), so downloads won't start: free some space,
lower the reserve, or move the staging folder to a bigger drive. Amber means it's getting close.

### A network folder PlexDL can't open

A folder on another PC (`\\PC\share\…`, such as the Inbox or a library folder reached over the network) that
PlexDL can't open. The message says which of these it is:

- **"… isn't answering"**: that PC is switched off, asleep or not on the network. Start it up; PlexDL tries
  again by itself.
- **"… is on, but isn't sharing files"**: turn on **File and Printer Sharing** on that PC (Windows Defender
  Firewall → Allow an app, Private networks).
- **"There's no PC called …"**: check the name, or use the PC's IP address instead.
- **"… answered, but wouldn't let PlexDL into the share"**: the share name is wrong, or that PC wants a login
  that the Windows account PlexDL runs as doesn't have ("PlexDL needs a login for …"). A restart of this PC
  often causes this: a connection you opened by hand in File Explorer is gone afterwards.
- **"Windows refused access"**: PlexDL got in, but its account isn't allowed to use that folder. Give it
  permission on the share *and* the folder (see [Plex on a different PC](07-plex-on-another-pc.md)), or give
  PlexDL a login for that PC.
- **"PlexDL's login for … didn't work"**: the login saved in PlexDL was turned down; the message says why (wrong
  user name or password, a locked or disabled account, or "Windows is already connected … under another user
  name"). After a wrong password PlexDL doesn't try that login again by itself: press **Change** or **Test**.
- **"There's no G: drive …"**: a mapped drive that's disconnected (open it in File Explorer to reconnect it), or
  PlexDL runs as a Windows service, which can't see drives mapped in File Explorer: use the network path
  (`\\PC\share`) with a login instead.

To let PlexDL in:

- **Give PlexDL a login for that PC** (works as a service too): press **Enter a login for …** next to the
  message, or add one under Settings → Import into Plex → Library folders → **Logins for other PCs**. Use an
  account on that PC that may use the share, such as `PLEXSERVER\sam`, and the PC's name or IP address exactly
  as it appears in the folder path. PlexDL keeps the password encrypted, signs in only when a folder there
  won't open without it, and uses the login for every folder on that PC (library folders, Inbox, Convert
  folders, backups, staging and overflow folders). Windows allows one user name per PC at a time, so it's one
  login per PC.
- **PlexDL running as you** (started by hand): a drive you've mapped in File Explorer works too; PlexDL
  suggests it under Library folders once it has found Plex's files on it.
- **PlexDL installed as a service** with its own account: alternatively, run the service as an account both PCs
  know, as described in [Plex on a different PC](07-plex-on-another-pc.md), steps 1, 2 and 4.

Then press **Look now** on the Inbox page, or **Check again** under Settings → Import into Plex.

## Downloads and imports

**A download keeps failing.** The Queue shows the reason and when it will try again. PlexDL retries on its own
(10 times over two days, then once a day for a week; Settings → Downloads), always carrying on from what it
already has. A friend being offline doesn't count: the download waits for them. **Keep for later** stops the
retries but keeps the part; **Retry** tries straight away.

## What the Queue says

### Waiting for window

Downloads are only allowed in certain hours (Settings → Downloads → Only download during a time window, or a
window for that friend). It starts by itself when the window opens; the top of the Queue says when.

### Waiting for a friend

The friend's server is offline, busy streaming to someone (if you set it to pause then; by default PlexDL slows
down instead and only the extra downloads wait), over the data limit you set for it, or resting after
errors. The line says which and until when. Nothing is lost: the download carries on where it stopped. Retries
aren't used up while a friend is offline. If another friend has a copy that's as good, the download moves to them
after 15 minutes; **From…** lets you choose another friend straight away (see
[When a friend is busy](03-compare-and-download.md#when-a-friend-is-busy-another-friends-copy)).

### Paused

You paused this download (or the whole queue), or chose **Keep for later**. **Resume** carries on from where it
stopped. "Pausing when these downloads finish" at the top of the Queue means the queue pauses once the downloads
running now are done; nothing new starts meanwhile.

### Needs disk space

PlexDL won't start a download that wouldn't fit with room to spare. Free some space, or change the reserve in
Settings → Downloads. It starts by itself once there's room. System → Storage shows when each drive will fill up.

### Access denied

The friend's server refused the download: they haven't allowed downloads for you, or stopped sharing that
library. Ask them to turn on **Allow Downloads** for you in Plex (or **Allow media downloading** on
Jellyfin), then press **Retry**.

### Flagged by Windows Defender

Windows Defender checks every download (and every file from the Inbox or a Convert folder) before PlexDL opens
it. This one was flagged, with the name of what Defender found: PlexDL didn't open it or add it to Plex, and
Defender has quarantined it as it does with anything it finds (**Windows Security → Virus & threat protection →
Protection history** shows it and lets you restore it if you're sure it's a false alarm). **Retry** downloads it
again (it's checked again); **Cancel** forgets it. Video files very rarely carry anything harmful, so a file that's
flagged again is best left alone, or downloaded from another friend with **From…**.

If the System page says **Malware scanning: Not scanning**, Windows Defender isn't available to PlexDL (another
antivirus is in charge, or Defender is turned off): downloads are converted without that check.

A file in a **Convert folder** that Defender flags is listed as skipped with the same reason (and you get a
notification); **Convert again** clears it from the list once it's gone.

### Failed

Something went wrong that PlexDL couldn't get round by itself; the red line under the title says what.

- **Downloading**: every retry failed, or the file is gone from the friend's server. **Retry** tries again,
  carrying on from what's already downloaded; **Keep for later** keeps it without retrying.
- **Converting**: "The downloaded file can't be read" (or "is missing") means the download was damaged:
  PlexDL has deleted it, and **Retry** downloads it again. Any other conversion failure, such as "Output check
  failed", is retried by converting the same download again, which helps when something on this PC got in the
  way. If it keeps failing, **Cancel** it and add the title again from Compare, picking another friend's copy
  if there is one.
- **Adding to Plex**: the library folder couldn't be written to or Plex didn't answer. Fix that (see
  [Library folders](#library-folders)), then **Retry**.

### Needs review

Plex matched the file to a different title, or the file looked wrong after converting. The Queue shows what
Plex chose with a link to it: fix the match in Plex and press **Mark as done**, or **Retry import**. A file that
couldn't be converted can be imported as it is or cancelled.

### Conversions paused

Your Plex server is transcoding for someone, and Settings → Conversion says to wait so viewers come first.
Re-encoding carries on when they finish; files that are only repackaged (video copied) carry on meanwhile.
**"ffmpeg isn't installed"**: install it in Settings → Conversion.

### Imports waiting

PlexDL can't add files to Plex right now: usually your Plex server isn't answering, or a library folder can't
be written to (see [Library folders](#library-folders); when it's on another PC, see
[A network folder PlexDL can't open](#a-network-folder-plexdl-cant-open)). They're added as soon as that's
fixed.

## Converting

### ffmpeg

If Settings → Conversion (or System) shows ffmpeg with a version number, it's installed and working;
**Install ffmpeg** again only downloads the same version. An amber **Video encoding** line is about the
graphics card, not ffmpeg (below). If installing fails, the reason shows under it: usually no internet
connection, or security software blocking the download.

### Video encoding

PlexDL tries your graphics card first (NVIDIA, Intel or AMD) and uses the processor when it can't. Converting
still works, it just takes longer: PlexDL then converts one file at a time at low priority (so Plex comes
first) and uses a faster setting for anything that would take over 3 hours. If the PC has no graphics card that
encodes video this is green and there's nothing to do. If it's amber, the line says why the card failed its
test: update the graphics driver if it says so, or if the card was busy (Plex may be transcoding on it) press
**Test encoders again** in Settings → Conversion once Plex is idle.

## Notifications and schedules

### Notifications

Amber means sending to Discord, ntfy or email failed last time; the line says why (a wrong webhook, topic or
password, usually). Fix it in Settings → Notifications and press **Send test**. Everything still shows under the
bell in PlexDL.

### Automatic syncs

Amber means the nightly full sync is turned off, so new titles on friends' servers only show up when you sync by
hand. Turn it on in Settings → Schedule.
## Opening PlexDL

**Setup says "PlexDL was copied but its service did not start".** Open
`C:\ProgramData\PlexDL\logs\install.log`: the last lines say why, including what PlexDL itself reported.
PlexDL 0.1.2 always failed here (a bug fixed in 0.1.3), so download the latest installer and run it again; it
repairs the existing install. If it still fails, send `install.log` and the `setup-…log` next to it with
**Feedback**, or by email. Silent installs end with exit code 20 in this case.

**PlexDL doesn't open.** Check the **PlexDL** service is running (Start → type "Services" → PlexDL → Start).
On the Plex server itself use `http://localhost:32500`.

**It opens on the server but not from other devices.** Use the server's name or IP address with port 32500.
The firewall option must have been ticked when installing (run the installer again to change it), and the
other device must be on the same home network.

**Port 32500 is in use.** Run the installer again and choose another port.

**"Can't reach your Plex Media Server" at sign-in.** PlexDL looks for Plex on the same PC. If Plex runs on
another PC, open `http://localhost:32500` on the PlexDL PC and use **Plex on another PC?** under the sign-in
button (see Installing → Plex on a different PC).

**"Plex.tv doesn't list … as an address of …".** Enter the address Plex itself reports: its private IP and port
from Plex → **Settings → Remote Access** (usually port 32400), not a name or port forward of your own.

**An import folder shows "may point at the wrong folder".** The folder mapping in Settings → Import into Plex
reaches a folder, but not the one Plex uses: the files Plex has there aren't at the mapped path. Fix the mapping
before importing.

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
