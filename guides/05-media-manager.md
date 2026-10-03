# Media Manager

Media Manager looks after **your own** library: names Plex may misread, duplicates, files Plex hasn't picked
up, wrong matches, files Plex has to convert to play, broken files, clutter and space you could free.

## It's safe by design

- **Scanning only reads.** Nothing changes until you choose a fix and confirm it.
- **Nothing is deleted.** Files that are replaced or removed move to the `PlexDL Backup` folder next to the
  library. The only exception is deleting old PlexDL backups, and only after you tick to confirm.
- **Every change can be undone** from the **Changes** tab.
- If PlexDL is stopped part-way through a fix, it puts the files back where they were when it next starts.

## Scanning

**Scan now** reads every library folder and compares it with what Plex has (a few minutes for a large
library). **Deep check** also looks inside every video with ffprobe to find broken files and audio or subtitle
problems; the first one takes a while (about half an hour for 12,000 files over the network), later ones only
read files that changed. You can turn on a **weekly scan** in Media Manager → Settings; it tells you about new
issues only.

## Working through the issues

The checks are grouped on the left (Naming, Duplicates & clutter, Plex, Playback & quality, Storage) with how
many each found. Pick one to see its issues. Each says what's wrong, why it matters, what the fix will do and the
exact files involved (**Details**).

- **Kind of problem** narrows a check down (for example *DTS/TrueHD audio only* or *Forced picture subtitle*
  under "Files Plex has to convert to play").
- Tick issues, or **Select all fixable on this page**, or **select all N in this list** (every issue matching your
  filters, not just the 100 on screen), then **Review & fix…** to see every change before it happens.
- Choose **Now** or **Later, at** a time (for example 02:00), so big jobs run overnight. Scheduled batches are
  listed at the top with **Cancel**.
- While a batch is running you can still add more: they wait their turn and start as soon as it finishes.
- **Dismiss** hides an issue you're happy with (it stays hidden after later scans; **Show dismissed** brings it
  back).

Conversions take time: a quick repackage of a TV episode takes a few minutes over the network; re-encoding a
film can take about an hour.

## Plex upkeep

The **Plex upkeep** box runs Plex's own maintenance: **Empty trash** (forget titles whose files are gone),
**Clean bundles** and **Optimise the Plex database**. Each shows its progress as Plex works, when it was last run
from PlexDL, whether Plex already does it by itself, and **Recommended** when there's a reason to run it now.

## If something was interrupted

If a fix couldn't be put back automatically after a restart (for example because a drive wasn't reachable), a red
box at the top lists what's left. PlexDL tries again every minute. If you sort the files out yourself, tick
**I've put these right by hand** and **Forget it**. New changes wait until then.

## Settings

Media Manager → Settings: file types never called junk (for example `nfo` if you keep those), how old PlexDL
backups must be before they're offered for deletion, when a film counts as "not watched for years", the weekly
scan, and whether 10-bit H.264 is converted to HEVC (smaller, plays on most TVs) or 8-bit H.264 (plays on older
devices too).
