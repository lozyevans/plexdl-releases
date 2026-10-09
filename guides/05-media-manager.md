# Media Manager

Media Manager looks after **your own** library: names Plex may misread, duplicates, files Plex hasn't picked
up, wrong matches, files Plex has to convert to play, broken files, clutter and space you could free.

![Media Manager after a scan: what it found, by kind, with a fix for each](images/media-manager.png)

## It's safe by design

- **Scanning only reads.** Nothing changes until you choose a fix and confirm it.
- **Nothing is deleted.** Files that are replaced or removed move to the `PlexDL Backup` folder next to the
  library. The only exceptions are deleting PlexDL's own backups, after you tick to confirm, and the nightly
  clean-up of old backups if you turn it on.
- **Every change can be undone** from the **Changes** tab, unless a file it changed has been replaced since (by a
  newer download, say): then Undo leaves the newer file alone and says so.
- If a scan finishes while you're reviewing fixes, **Apply** stops and asks you to look again, so only what you
  saw is changed.
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

**Empty folders** are checked twice. The fix looks at the whole folder again first and refuses if anything is in
it now. Then it removes the folders one by one, deepest first, in a way that stops at any folder that isn't
empty. So a file copied in at that moment stops the removal; it's never deleted with the folder. Removed folders
come back with **Undo**. "Empty" means no files at all: a folder with only a `Thumbs.db` or a subtitle in it isn't
listed. A show folder can end up empty when its episodes were moved or deleted outside Plex. Check
**Files Plex can't find** for that show before removing it.

## Duplicates

**Duplicates & clutter → Duplicates** finds a film or episode you have more than once: several versions under one
Plex title, the same title in two of your libraries, or byte-for-byte copies. The fix keeps the best copy and
moves the others to backup. A copy only counts as a duplicate when nothing is lost by moving it:

- It's the **same cut** as the copy kept (running times within 4 minutes or 4%), the same **edition**
  (`{edition-…}` in the name) and both are 2D. A 3D copy (in a 3D library, or `3D`, `SBS` or `HSBS` in the name)
  is never a duplicate of the 2D one.
- It's a plain copy of **that one episode**: a file named as another episode, or holding two (`S01E01-E02`), is
  left alone, as is a file another title still uses.
- It's **another file**: the same file reached through two library folders (or a folder link) is listed as
  "Same folder in two libraries", with nothing to move.
- The copy kept is **complete and readable**: never CD2 on its own, a file smaller than Plex saw, or one Deep
  check couldn't read.

Each fix names the copy it keeps. Just before it runs it checks again: the copy kept must still be there,
unchanged and a different file, and the copies going must be unchanged since the scan. Byte-for-byte copies are
compared in full first. If anything is different, nothing moves and you're asked to scan again. A batch scheduled
for later skips any issue you've dismissed since, or whose fix a later scan changed.

### If you used Duplicates before 0.1.7

Earlier versions could treat copies as duplicates when they weren't (the same film in Films and Kids Films, a 3D
copy, another edition, a file holding two episodes) and move them to the `PlexDL Backup` folder. To put them all
back so 0.1.7 can check them again with its safer rules, use `undo-duplicate-fixes.ps1` (in PlexDL's `scripts`
folder, or from the release page):

1. Open PowerShell as an administrator.
2. Run `.\undo-duplicate-fixes.ps1` on its own first. It only reports, for each change, whether its files can go
   back. Nothing changes.
3. Run `.\undo-duplicate-fixes.ps1 -Restore`. It stops PlexDL, copies PlexDL's database aside first, moves every
   backed-up copy back to where it was (never over anything), marks those changes as undone and starts PlexDL
   again. A report is saved next to the database.
4. In Plex, run **Scan Library Files** on the folders it lists, then run a new Media Manager scan in 0.1.7.

Copies whose backups were already deleted can't come back; the report lists them so you can check those titles.

## Night shift

For the long jobs (the files Plex has to convert to play, and files that could be much smaller), turn on
**Night shift** in Media Manager → Settings and choose a window, for example 01:00 to 07:00. Every night in that
window, Media Manager converts those files one at a time, the most serious first, until there are none left. It
doesn't start a new one after the window ends; one already running finishes. A file that can't be converted is
skipped for the rest of that night. You get a summary each morning that it did something, and a note when it's
all done; a later scan that finds more gets picked up the next night. The top of the page shows how many are
left. Every conversion is in **Changes** with **Undo**, like any other fix.

## Plex upkeep

The **Plex upkeep** box runs Plex's own maintenance: **Empty trash** (forget titles whose files are gone),
**Clean bundles** and **Optimise the Plex database**. Each shows its progress as Plex works, when it was last run
from PlexDL, whether Plex already does it by itself, and **Recommended** when there's a reason to run it now.

## PlexDL backups

Files that PlexDL replaces (upgrades, fixes) or takes out (History's Undo) go to a `PlexDL Backup` folder next to
each library. The **PlexDL backups** box (under Plex upkeep) shows how much space they take, how much of that is
older than the age set in Settings (30 days to start with), and the free space on each drive. **Check again**
looks afresh; otherwise it's checked every 10 minutes when you look.

- **Delete older than 30 days** deletes just the old ones.
- **Empty now…** deletes everything in the backup folders.

Both ask you to tick **I understand this can't be undone** first: once a backup is gone, the change that put it
there can't be undone any more. Each backup is checked again just before it's deleted, and anything that changed
since is left alone. If more backups have appeared since you looked, nothing is deleted and the new figures are
shown for you to confirm again. Nothing outside the backup folders is ever touched, and only folders PlexDL made
are counted: anything else you keep in there is left alone. A backup folder set in Settings that holds a library
folder isn't used (PlexDL uses `PlexDL Backup` at the top of the drive instead). Entries under Changes whose
backups are deleted are marked as no longer undoable. A backup that holds the only copy of a film or episode whose
upgrade hasn't finished (it failed part-way, say) is never deleted until you retry or cancel that download.

To keep them in check by themselves, turn on **Delete PlexDL backups older than N days by itself, each night** in
Media Manager → Settings. Once a night (after 03:00) PlexDL deletes the old ones and tells you how much it
freed. It's off until you turn it on.

## If something was interrupted

If a fix couldn't be put back automatically after a restart (for example because a drive wasn't reachable), a red
box at the top lists what's left. PlexDL tries again every minute. If you sort the files out yourself, tick
**I've put these right by hand** and **Forget it**. New changes wait until then.

## Settings

Media Manager → Settings: file types never called junk (for example `nfo` if you keep those), how old PlexDL
backups must be before they're offered for deletion, when a film counts as "not watched for years", the weekly
scan, and whether 10-bit H.264 is converted to HEVC (smaller, plays on most TVs) or 8-bit H.264 (plays on older
devices too).
