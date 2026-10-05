# PlexDL

PlexDL compares the Plex libraries your friends share with you against your own Plex, shows exactly which
films, shows, seasons and episodes you're missing (and which of yours a friend has in better quality), then
downloads them, converts them so they play everywhere, and adds them to the right library in your Plex. It also
tidies your own library (**Media Manager**), safely and with undo.

It runs on the Windows PC that runs your Plex Media Server, as a service, and you use it from any browser on
your home network.

## Download

**[Download the latest version](https://github.com/lozyevans/plexdl-releases/releases/latest)**: under **Assets**, download
`PlexDL-Setup-0.1.3.exe` (and `.sha256` if you'd like to check it).

Needs 64-bit Windows 10, 11 or Server 2016 or newer, with Plex Media Server installed on the same PC. Nothing
else to install: the installer brings everything PlexDL needs.

## Install in short

1. Run `PlexDL-Setup-x.y.z.exe` **on your Plex server** and allow it to make changes. If Windows says
   "Windows protected your PC", choose **More info → Run anyway** (the installer isn't code-signed yet).
2. Click through: it checks the PC first and tells you if anything needs fixing.
3. Your browser opens PlexDL. **Sign in with Plex** using the account that owns the server, and follow the
   setup checklist.
4. On the Dashboard press **Full sync** once, then look in **Compare**.

Upgrading: run the newer installer the same way; your settings and history are kept, and if the new version
doesn't start the old one is put back.

## Guides

- [Quick start](guides/01-quick-start.md)
- [Installing and upgrading](guides/02-install.md)
- [Finding and downloading](guides/03-compare-and-download.md)
- [Following shows and automation](guides/04-automation.md)
- [Media Manager](guides/05-media-manager.md)
- [Troubleshooting](guides/06-troubleshooting.md)

The same guides are inside PlexDL under **Guides**.

## Good to know

- PlexDL only downloads what server owners have allowed you to download, and only from Plex and Jellyfin
  servers shared with you. It never downloads from Netflix, Disney+ or other streaming services.
- Nothing is deleted from your library: anything replaced or removed goes to a `PlexDL Backup` folder, and
  changes can be undone.
- PlexDL isn't made by, endorsed by or connected with Plex Inc. or the Jellyfin project.
- Problems or ideas: use **Feedback** in PlexDL (top right). It saves a zip with the details (passwords and
  tokens removed) to send to whoever shared PlexDL with you.

Licence: [MIT](LICENSE). Third-party notices are installed with PlexDL (Start menu → PlexDL).
