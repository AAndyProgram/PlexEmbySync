# About

Program to synchronize playback from Plex to Emby and vice versa

**You don't need a Plex Pass or Emby Premiere to use this program.**

**This is a multi-user program.**

**The program closes to the system tray. To close the program, right-click the icon on the taskbar.**

The program only works with Windows. There is no need to run the program directly on the Plex/Emby server (if your server is Linux based). You can run it from any computer on the local network.

Do you like this program? Consider adding to my coffee fund by making a donation to show your support. :blush:

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/andyprogram)

**Bitcoin**: bitcoin:BC1Q0NH839FT5TA44DD7L7RLR97XDQAG9V8D6N7XET

# What can program do
- Monitoring Plex playback activity and set the same playback state of that item in Emby *(synchronization of playback progress and/or setting the states Watched/Unwatched)*
- Monitoring Emby playback activity and set the same playback state of that item in Plex *(synchronization of playback progress and/or setting the states Watched/Unwatched)*
- Periodic libraries updates (only different playback states and/or Watched/Unwatched statuses)
- Periodic playlists updates
- Update libraries on demand (two modes):
  - ```Different only``` - only different playback states and/or Watched/Unwatched statuses
  - ```Full updating``` - all items will be updated
- Update playlists on demand
- If you start playing the 1-st episode of the 1-st season, the program can set the status to Unwatched for all other episodes of the TV-Show being played

# What for
- If you use both servers together, this is extremely convenient.
- **If the internet is down and you can't connect to the Plex server**
- *If you want to test a new server (for example, you use Plex and want to try Emby)*

# Requirements
- Windows 7, 8, 9, 10, 11 with **NET.Framework 4.6.1** or higher (v4.6.1 must be installed)
- Same local network with the server
- Plex and Emby **must** have the same file paths
- Plex/Emby server operating system: **Windows**, **Linux**
- Both servers **must** be running the same operating system

# Server Settings

The program configuration is stored in the ```Settings``` folder. To clean up the configuration, you can delete ```Settings``` folder.

## Using the Start Assistant

Just open ```Settings``` - ```Start Assistant``` and fill in the fields. Each button has a step number. The next button will be activated after the step is completed.

## Using advanced settings

### Setup Plex
- Requirements
  - Plex user account with admin rights
  - Plex IP address
  - Plex web UI port (Default 32400)
  - Plex server ID[^2]
  - Plex **admin** [token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)[^1]
- In the app, open ```Settings``` - ```Plex Server Settings```
  - Fill the IP address
  - Fill the port.
  - Fill the **admin** token
  - Click the curved arrows in the ```Server``` field. It will autofill itself

### Setup Emby
- Requirements
  - Emby user account with admin rights
  - Emby IP address
  - Emby web UI port (Default 8096)
  - Emby server ID[^3]
  - Emby API key
    - In Emby, go to ```Dashboard``` - ```Advanced``` - ```API Keys```
    - Click the ```New API key``` button
    - Name the new API key any descriptive name, e.g. ```Plex-Emby Sync```
    - Copy the newly created string up to the part with the above descriptive name (e.g. for ```axxxxxxxxxxz - Plex-Emby Sync``` we only need the ```axxxxxxxxxxz``` part)
- In the app, open ```Settings``` - ```Emby Server Settings```
  - Fill the IP address
  - Fill the port
  - Fill the API key
  - Click the curved arrows in the ```Server``` field. It will autofill itself

### Get users

*Users will be automatically collected when the form is opened.*

- Plex
  - In the app, open ```Settings``` - ```Users``` - ```Plex```
  - Check users for the admin flag to make sure the flag is set for admin only
  - Set a **[token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)** for each user
  - If you want to use playlist sync, you **must** also set up a ```Playlist tag``` for Plex users
- Emby
  - In the app, open ```Settings``` - ```Users``` - ```Emby```.
  - If you want to use playlist sync, you **must** also set up a ```Playlist tag``` for Emby users

### Bind users

Each user on each platform has their own set of watch states. This step associates the users we need to sync with their counterpart.
- In the app, open ```Settings``` - ```Users``` - ```Associations```.
- Click ```Add``` to add a binding. You **must** select a Plex user and an Emby user. ```Friendly name``` is only used by this application (PlexEmbySync).

### Bind libraries.

*Libraries will be automatically collected when the form is opened.*

At this point, you **must** configure which libraries to sync.
- In the app, open ```Settings``` - ```Libraries```.
- Click ```Add``` to add a binding. You **must** select a Plex library and an Emby library.
- Click the ```Update Plex/Emby paths``` buttons to make sure that all server library media paths are added.

**It's all! The program is ready to go!**

If you wish, you can configure the [global settings](#program-settings) of the program.

# Program settings

## Main settings
- ```Priority Server``` - default server for full library and playlists updating (default Plex)
- ```Check version at start``` - check for a new version when starting the program
- ```Run monitoring at start``` - automatically start playback monitoring and sync on startup
- ```Linux Servers``` - Emby and Plex are installed on the Linux operating system
- ```Start show detecting``` - if you start playing the 1-st episode of the 1-st season, the program can set the status to Unwatched for all other episodes of the TV-Show being played
- ```AutoUpdate``` - periodic full auto-updating of libraries with an interval (minutes)
- ```CPU Usage``` (default - ```Auto```) - how the program works when updating libraries:
  - ```Auto``` - the program will detect heavy work (like transcoding) and decide which update model to use;  
  - ```High``` - the maximum amount of CPU resources will be used to update the libraries;  
  - ```Low``` - the minimal amount of CPU resources will be used to update the libraries.
- ```Sleep hours``` - this option works with CPU usage mode ```Auto```

## PlayLists settings

*The default update respects ```Priority Server``` (**Source**)*

**To work with updating playlists, you must set an ```Owner``` (playlist ```Tag``` field in Emby) for each playlist you have, and this ```Tag``` you must add to the [Plex and Emby user](#get-users)**

**To sync shared playlists (no owner in Emby), you must add ```Shared playlist``` to the title or summary field in Plex. This playlist must not contain any tags in Emby!**

- ```Emby playlists path``` - Path to [Emby playlists](https://support.emby.media/support/solutions/articles/44001849016-playlist-manual-migration)[^4]
- ```Backup playlists``` - playlist backup directory where playlists will be backed up before changes are made
- ```Update playlists during full update``` - playlists will be updated during library update
- ```AutoUpdate``` - playlists will be periodically updated at the specified interval (minutes)
- ```Remove missing``` - delete playlists not found in source
- ```Remove playlists with no owner``` - delete playlists without ```Owner``` tag
- ```Remove empty playlists``` - delete all empty playlists
- ```Keep Emby tags``` - keep all Emby tags (not just ```Owner```)
- ```Keep Emby other fields``` - keep all other Emby fields (e.g. rating, genres)

# Buttons
- ```Start/Stop``` - start/stop activity monitoring
- ```Full library updating```:
  - ```Full update```, ```Playlists update```:    
    - ```Default``` - force update of the library/playlists by your chosen ```Priority Server```;	
    - ```Plex to Emby``` - force update Emby library/playlists with Plex library/playlists;	
    - ```Emby to Plex``` - force update Plex library/playlists with Emby library/playlists.	
  - ```Stop``` - stop updating.

[^1]: This token must be owned by the primary Plex user (administrator). To make sure you get the token you need, you must switch the user to your account (administrator). If you are the only Plex user, then this is the token you need.

[^2]: Open any Plex item (TV-Show/Episode, Movie). Look at the address bar: https://app.plex.tv/desktop/#!/server/```ServerID```/details?

[^3]: Open any Emby item (TV-Show/Episode, Movie). Look at the address bar: http://1.1.1.1:8096/web/index.html#!/item?id=11111&serverId=```ServerID```

[^4]: If PlexEmbySync is not running directly on the server, you must specify a remote path to the playlists to allow the program to access them.