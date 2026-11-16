# MxScout - Release Notes

## MxScout 1.22.1  (November 15, 2026)
- FIXED: playback via camera showed nothing on cameras whose factory IP address MxScout couldn't read (seen on an M25 with firmware MX-V4.7) - it never got as far as the recordings. It no longer needs that address at all.
- Playback via camera now asks the camera directly "which recording starts at this time?" - one small request, answered with the recording's number and exact start. An hour of timeline costs two such requests, and a recording's whole video comes in one request. Much less back-and-forth than before, which matters over a slow site connection.
- The timeline looks up several hours at once instead of one after the other.
- The recording-folder way (as MxControlCenter does it) is kept as the spare for cameras that don't answer the time question.
- Check Playback Via Camera now finishes by really doing it: it lists the recordings of an hour and loads one, and says how long that took.

## MxScout 1.22.0  (November 15, 2026)
- Playback VIA CAMERA now works the way MxControlCenter does it - including continuous recording. MxScout reads the camera's own recording folders through the camera's web port (the same folders that are on the file server), so every recorded minute shows on the timeline and plays, not just alarms. Nothing to set up: it needs only the camera's login, and works for cameras at remote sites.
- How it finds a moment: the camera has no list of which recording is when, so MxScout looks at a recording's time, sees whether that is too early or too late, and tries again closer - a handful of small requests. Times it has learned are remembered, so moving around the same day gets quicker. The first jump to a new day takes a few seconds.
- Each recording is fetched in pieces, three at a time. Over a slow site connection a minute of video can take several seconds to arrive.
- Cameras that don't publish their recording folders (for example recording only to internal memory) still use the camera's alarm list, as before.
- Check Playback Via Camera now also tests this: whether the folders are there, and which recording it finds for 30 minutes ago and 26 hours ago.

## MxScout 1.21.4  (November 15, 2026)
- FIXED (playback via camera, real cameras): MxScout now reads the camera's own answers correctly - the oldest and newest recording (it used to take the newest for both, so the timeline covered almost nothing) and the camera's list of recordings (each entry carries a small list of its own, which made MxScout skip every entry). Event recordings (alarms) now show on the timeline and play.
- Not done yet: footage a camera records CONTINUOUSLY between events doesn't show via the camera yet - the camera's list only names alarms. The two tools below are for working that out.
- NEW: right-click a camera > Record What MxControlCenter Asks This Camera. A recorder stands in for the camera on this PC (127.0.0.1 and the port shown); point MxControlCenter at it, play recordings back via camera, and every request it makes is listed, ready to copy. Everything is passed to the real camera unchanged; passwords are never written down; only this PC can reach it.
- Check Playback Via Camera asks the camera a few more questions (details of a finished recording, and which recording was running at a given time).

## MxScout 1.21.3  (November 15, 2026)
- NEW: right-click a camera > Check Playback Via Camera. When playback via the camera shows nothing, this asks the camera for its recordings step by step - the same requests Playback makes - and shows how the camera answers each one, with a plain-English result at the bottom. Copy Report copies it all (no passwords) to paste into a message.

## MxScout 1.21.2  (November 15, 2026)
- Via camera is now the default: every camera you add - local or remote - is set to Access recordings: Via camera. It works everywhere the live picture works, with nothing else to set up.
- Cameras you already have keep their setting. To switch them: select them in VIDEO SOURCES (Ctrl+A for the whole tab), right-click > Access Recordings > Via Camera. For a camera on your own network whose recording folder this PC can open, Default recording path is faster.

## MxScout 1.21.1  (November 15, 2026)
- Camera Properties now shows where recordings come from the way MxControlCenter does: a framed line "Access recordings: Via camera" (or Default recording path / Specific recording path) with a Change... button.
- Change... opens "Access Recordings of [camera]" with the three choices: Via camera; Default recording path (the camera's folder in your Recording Locations - it shows the folder it found); Specific recording path with Browse. A check box says what to do when a path can't be opened from this PC: go via the camera instead (the default), or show nothing.
- The right-click menu in VIDEO SOURCES uses the same words: Access Recordings > Via Camera / Default Recording Path / Recording Path Only.

## MxScout 1.21.0  (November 15, 2026)
- Cameras at remote sites now play their recordings back THROUGH THE CAMERA, automatically. A remote camera records to a file server at its own site, and no UNC path or mapped drive reaches that from this PC - so MxScout asks the camera for the recordings instead, over the same connection as the live picture. Cameras added with "At a remote site" (or by a public address / forwarded port) are set to Playback from: Through the camera when they are added.
- Remote cameras you added with an earlier version are switched over once, the first time this version starts. Anything you set by hand in Camera Properties is left alone.
- Adding remote cameras no longer asks "These cameras say they record to \\server\share - add it?" - that share can't be opened from here.
- NEW: right-click cameras in VIDEO SOURCES > Playback From > Through the Camera / Automatic / Recording Folder Only. Works on many cameras at once: select them with Ctrl or Shift (Ctrl+A for the whole tab). Takes effect right away.

## MxScout 1.20.0  (November 15, 2026)
- NEW: Scan for Cameras is now a step-by-step wizard, with the steps shown across the top and Back / Next at the bottom:
- NEW: Totals above the camera list - Found, Ready, Password needed, Different subnet, Problem, Already in MxScout, New and Ticked to add - counting up live while the scan runs. Click a total to select those cameras: for example click Password needed, then Set Password, to give them all their login in one go.
- Tick All New and Untick All buttons under the list. The Next button shows how many are ticked.
- Scanning again (or scanning the same site twice) refreshes the cameras already in the list instead of listing them twice, and keeps your ticks. Going Back never loses what was found.
- The scan no longer starts by itself when the window opens: step 1 shows what will be scanned first, and one click on Scan (or Enter) starts it.
- Pending Adoption uses the same window, starting at the list.

## MxScout 1.19.1  (November 15, 2026)
- Scan for Cameras: new "Log in with" boxes - User and Password - next to the scan button. Type the login your cameras use and MxScout tries it on every camera the scan finds, so they show up ready (green dot, name, model, preview) instead of "Password needed". Works for both kinds of scan and for Add by Address. Cameras with a different login still show Password needed - select them and click Set Password.
- At a remote site the login is remembered with the site (the password encrypted for your Windows account): picking the site under Saved sites fills in the address, the ports and the login.

## MxScout 1.19.0  (November 15, 2026)
- Scan for Cameras now asks one clear question at the top: Where are the cameras? - "On this network" or "At a remote site (another location, over the internet)". Choosing the remote site puts its boxes right in the window: Address, Ports from / to, Site name and your Saved sites. Example: address 108.170.94.18, ports 10000 to 10254, then click Scan Site (or press Enter). Every camera that answers is listed with its port, ready to tick and add. (The old Scan Remote Site button and its separate window are gone.)
- Paste shortcut: paste "108.170.94.18:10000-10254" or "108.170.94.18 10000 10254" into Address and the port boxes fill themselves in. The window shows how many ports will be tried.
- NEW: Add to tab (bottom of the Scan window). Choose which location tab the ticked cameras - and the new layout - go on, or pick "(new tab...)" to make one on the spot; a remote site's name is offered as the tab name, and a site whose name matches a tab picks that tab by itself. The main window switches to that tab when you close the scan.
- The Scan window opens the way you used it last, with your last site filled in. Sites are remembered when scanned - scanning one again later is pick it under Saved sites, click Scan Site.

## MxScout 1.18.0  (November 15, 2026)
- NEW: Location tabs. A row of tabs across the top of the window, one per location - a building, a store, a customer site, or anything else you want to keep apart. Each tab has its own cameras (VIDEO SOURCES) and its own LAYOUTS; click a tab and the left panel swaps to that location and the layout you had open there last comes back. Click [+] to add a tab.
- Your existing cameras and layouts are all on the first tab, called Main (double-click a tab to rename it). To split them up: add a tab, then drag cameras from VIDEO SOURCES or a layout from LAYOUTS onto it - or right-click them and choose Move to Tab. A layout takes its cameras along.
- Cameras you add (Scan for Cameras, Scan Remote Site, Add Camera by Address) land on the tab that is open.
- Each tab shows how many cameras it has, and a red dot when cameras at that location aren't answering - so you can see trouble at another location without switching to it.
- Right-click a tab to rename it, move it left or right, or delete it (drag tabs to reorder too). Deleting a tab never deletes cameras or layouts - they move to the tab next to it. Ctrl+Tab and Ctrl+Shift+Tab step through the tabs; Ctrl+T adds one.
- With Users and Rights on: adding, renaming and moving tabs needs the Edit Layouts right, and a user only sees the tabs that have cameras they are allowed to see.

## MxScout 1.17.0  (November 11, 2026)
- NEW: MxScout Setup can install for ALL USERS of a PC. The installer now asks who MxScout is for. "Just for me" is what it did before (your own Windows account, no administrator). "All users of this PC" installs in C:\Program Files\MxScout, where only an administrator can change the program - the usual way on business and shared PCs, and the one security software expects. Everyone who signs in gets the shortcuts; each person keeps their own cameras, layouts and settings.
- For RMM tools: MxScout-Setup.exe /S /ALLUSERS installs for the whole PC without any windows. Run by the SYSTEM account (as RMM agents do) it chooses All users by itself.
- Updating an all-users install: Update now downloads the new installer, checks it, and Windows asks for an administrator's permission to put it in. MxScout then restarts as you. Just-for-me installs and the portable MxScout.exe update themselves as before.
- An installed MxScout now has its video engine (ffmpeg.exe, used for MP4 export) as an ordinary file next to the program, instead of unpacking it the first time you export. The installer is about 10 MB smaller too.
- Switching from Just for me to All users removes the per-user copy, so there is only ever one MxScout. Your data is kept.

## MxScout 1.16.0  (November 11, 2026)
- NEW: Scan Remote Site (Scan for Cameras > Scan Remote Site...). Finds the cameras at another location that are reached through port forwarding: type the site's public IP address or DNS name and the range of ports its router forwards to the cameras - for example 50.243.70.9, ports 10000 to 10255. MxScout tries every port (16 at a time) and lists each MOBOTIX camera that answers, with its name, model and its own MAC address, ready to tick and add like any other camera. Sites are remembered, so scanning one again is a click.
- Cameras that share one address on different ports are kept strictly apart everywhere - in the list, when adding, in the settings history and in the safe-change checks. Video Sources shows address:port for them.

## MxScout 1.15.0  (November 10, 2026)
- NEW: MxScout now comes two ways - the same program either way:

## MxScout 1.14.2  (November 10, 2026)
- The File menu showed the Settings shortcut as "Ctrl+Oemcomma" (Windows' internal name for the comma key). It now reads Ctrl+, .

## MxScout 1.14.1  (November 10, 2026)
- FIX: no live sound - Sound Check showed "can't get sound: (401) Unauthorized". The sound connection logged in to the camera differently from the picture connection, and some MOBOTIX cameras refused it. It now logs in exactly like the picture does (and tries the camera's other login method by itself if needed).

## MxScout 1.14.0  (November 10, 2026)
- NEW: Users and Rights (File > Users and Rights), modeled on MxControlCenter. Off until you switch it on.
- American spelling throughout (color, center, gray).

## MxScout 1.13.1  (November 8, 2026)
- FIX: the Softbuttons panel could show only "Edit..." (an empty button list was kept instead of the starting set). The MxCC-style buttons now always appear until you save your own list.
- The Softbuttons editor is laid out properly: the list on the left shows each button as it looks (color and name), with Add / Remove / Up / Down underneath; on the right Name, Color (swatches + More...), Show on, What it does and only the fields that apply - no gaps - plus a "Looks like" preview, what it does, and Test.
- The line under the softbuttons says whether the camera's own softbuttons were found. Right-click it (or the Softbuttons bar) > Show What the Camera Has for Softbuttons... shows the camera's softbutton settings (passwords hidden) with Copy All - paste that to Dialsoft if your camera's own buttons don't appear, so MxScout can read its layout.

## MxScout 1.13.0  (November 8, 2026)
- Softbuttons now look and work like MxControlCenter's: one full-width button per row, colored like MxCC (color in the middle fading to white): Admin Menu, Setup Menu (open the camera's own menus, logged in), Arm & Record, Audio on, MxPEG on / off (red), LEDs Blink, Play Sound (yellow), Play Last Event, Event List (green), 1x Zoom, Zoom +, Zoom -, Center Pan (blue), Normal Image, Surround Image (180/360 cameras), plus Snapshot and Instant Replay. The camera's own softbuttons follow, marked •. More than nine scroll.
- The left panel's sections have MxCC-style title bars with a [-] / [+] box; click a bar to fold that section away or open it again.
- The Video Sources columns always fit the panel (no sideways scroll bar).

## MxScout 1.12.0  (November 8, 2026)
- NEW: SOFTBUTTONS section in the left panel (above PTZ) - colored one-click buttons for the active tile's camera, like the softbuttons down the left of a MOBOTIX camera's own Live page:

## MxScout 1.11.4  (November 8, 2026)
- The left panel's sections fold away: click the LAYOUTS, VIDEO SOURCES or PTZ bar (▾ open / ▸ folded) to minimize that section - the others get the room. Click again to open it. Remembered.

## MxScout 1.11.3  (November 8, 2026)
- FIX: no sound at all. Since 1.10.2, a camera's sound stopped for good once you had clicked another tile (or switched modes) - going back to it stayed silent, so after a few clicks no camera gave sound. Now sound comes back every time you click a tile, and there is never more than one sound connection per camera.

## MxScout 1.11.2  (November 8, 2026)
- Healing mode also learns the MAC address of cameras that were added by IP address and are behind a router (it asks the camera itself), so they too are found again and keep their place in every layout when their IP address changes.

## MxScout 1.11.1  (November 8, 2026)
- NEW: Home view. A blue ⌂ Home button appears in the top-right corner of any zoomed tile (zoomed In MxScout, or the camera's own vPTZ moved by MxScout) - one click puts it back to the camera's normal full picture (1x, centered). Also: the ⌂ Home button on the PTZ panel (was "1x"), right-click a tile > Return to Home View, or press the Home key for the active tile.
- Updates: each version now downloads from its own address, and MxScout tries up to 3 times if a download comes back the wrong size (the update server can briefly hand out the previous version right after a release - that caused "the download is the wrong size").

## MxScout 1.11.0  (November 8, 2026)
- NEW: PTZ panel, docked in the lower left under Video Sources (like MxControlCenter). It works on the active tile (click a tile):

## MxScout 1.10.2  (November 8, 2026)
- FIX attempts for sound going silent:
- NEW: Help > Sound Check (also under Playback). Shows live where the sound stops - no sound device, muted, no tile selected, camera not sending sound, or sound arriving - with a Play Test Beep button and Reconnect Sound Device.

## MxScout 1.10.1  (November 8, 2026)
- Two clear restart choices everywhere: right-click a camera > Save Settings and Restart Camera... (saves the settings permanently, then restarts - the usual choice) or Restart Camera... (just restarts; unsaved settings are lost). Camera Settings has Save & Restart and Restart buttons, and Camera Actions uses the same names. Each shows its steps in the progress window until the camera is back.
- FIX: in Camera Settings the Apply Changes button could be pushed off the edge of the window by the new buttons. Apply / Undo now have their own row and are always visible.

## MxScout 1.10.0  (November 8, 2026)
- NEW: Restart Camera... right on a camera's right-click menu, and a Restart Camera button in Camera Settings (asks whether to store the settings first). Camera Actions > Store Settings and Reboot is still there too.
- NEW: Progress for every change. Saving settings, Restore, Store, Restart and Set Network Address open a window listing each step in order - safety check, backup, send, read back, store, restart, "waiting for the camera to come back... 34 s", backup afterwards - each with a spinner while it runs, a green tick when done or a red cross with the reason, and how long it took. It closes itself 3 seconds after success (untick the box to keep it open); after a problem it stays open.
- NEW: Configuration repository - every camera's settings history, kept automatically in MxScout's own data folder (%AppData%\Dialsoft\MxScout\Config Repository; Settings > Start-up can move it, e.g. to a NAS). A version is saved before and after every change MxScout makes, when a camera is added, and by a daily check of every camera - which also catches changes made in the camera's own web pages (marked "changed outside MxScout", with a note in the status bar). Only real changes become new versions. Right-click a camera > Configuration History (or History... in Camera Settings) shows each version and exactly which settings changed, compares with the camera now, saves a version as .cfg, or restores it. Backups made by older versions are brought in automatically.

## MxScout 1.9.0  (November 8, 2026)
- NEW: Set Network Address (Scan for Cameras). Give a camera an IP address on your network - e.g. a new camera still on its factory 10.x address, listed as "Different subnet". Select it and click Set Network Address...: MxScout briefly adds a matching address to this PC (Windows asks for permission once), saves a backup of all the camera's settings, shows you exactly what it will change and asks, writes the new address, restarts the camera and waits for it at the new address. The extra PC address is removed again straight away. Find a Free One suggests an unused address.
- NEW: Healing mode (Settings > Start-up, on). When a camera stops answering, MxScout hunts for it by its MAC address - this PC's network table, Bonjour and a quick sweep - right away, then after 30 s, 2 min and every 5 min. Found at a new IP (e.g. the router gave it another one): the camera is updated and reconnects by itself; the status bar says what happened. Found on a different subnet: the tile says so. MxScout also learns the MAC of cameras added by IP while they're online.
- Each tile's name bar now shows the camera's IP address next to its name.
- NEW: Camera Actions > Store Settings and Reboot... - makes the camera's current settings permanent and restarts it (backup taken first). Store Current Settings Permanently and Reboot Camera are still there on their own.
- NEW: Safe-change checks. Before any change to a camera (Camera Settings, Restore, Store, Reboot, Set Network Address) MxScout:

## MxScout 1.8.1  (November 8, 2026)
- FIX: live sound cut in and out once a second. The camera sends its sound in bursts of about a second, and MxScout's sound queue held less than that, so part of every burst was lost. Sound is now collected and played out evenly (about a second behind the picture) and the sound queue holds 3 seconds. Measured: 8 seconds of sound in 8 seconds, no gaps.

## MxScout 1.8.0  (November 8, 2026)
- NEW: Sound. You hear the camera of the active tile (the one you clicked) - its name bar shows a speaker:

## MxScout 1.7.2  (November 8, 2026)
- Tiles in playback stand out: a deep red name bar reading PLAYBACK with the recording's date and time, and a red video-tape icon in the top-right corner of the picture (like MOBOTIX software). Live tiles keep the dark gray bar with the red LIVE badge.
- The play-control tooltips also open when the mouse enters a button (more reliable on some Windows setups).
- MxScout now checks for updates every 30 minutes (was every 6 hours) and shows its version in the window title.

## MxScout 1.7.1  (November 8, 2026)
- FIX: the play controls had no tooltips. Their tooltips are now drawn by MxScout itself, just above the button the mouse is on, instead of by the Windows tooltip control (which first blinked there and then didn't appear at the bottom of the window). They never take the focus or the clicks, and close when you move away, switch programs or move the window.
- Tooltips on the play controls describe the per-tile playback correctly (they still said all cameras play in sync).

## MxScout 1.7.0  (November 8, 2026)
- CHANGED: Playback is now per tile. Playback (F6) puts only the SELECTED tiles into playback - every other tile keeps showing live video. Live (F5) puts the selected tiles back to live. Each tile's name bar says LIVE or PLAYBACK, and the status bar says how many tiles are playing back. The play controls appear while any tile is in playback; All Live (on the play controls) puts every tile back to live. Recordings-only sources (folders, .mxg clips) are always in playback.
- The play controls fit on smaller and 150%-scaled screens again (Export and All Live were being pushed into the overflow arrow).

## MxScout 1.6.0  (November 8, 2026)
- CHANGED: in Playback the play controls and the timeline now move only the SELECTED tiles (yellow frame) - not every tile. Click a tile to control just that one; Ctrl+click to add or remove tiles; Ctrl+A selects them all. The other tiles stay frozen on their own moment, so you can compare different times side by side. Clicking a tile jumps the timeline to that tile's moment; tiles you add with Ctrl+click join the moment the selection is on.
- NEW: Link All switch on the play controls - every tile follows one shared timeline again (like MOBOTIX MxControlCenter).

## MxScout 1.5.4  (November 8, 2026)
- FIX: fast forward and rewind at 16x and above showed "No preview available". At those speeds MxScout used to show each recorded minute's small preview picture (INFO.jpg), which many cameras fill with that placeholder. It now shows the real video, smaller and skipping frames so it keeps up. Placeholder pictures are ignored everywhere (Add Recordings preview, Live-mode stills too).

## MxScout 1.5.3  (November 8, 2026)
- FASTER PLAYBACK of big cameras. Measured on a 6-megapixel recording: a large single-camera tile went from about 6 to the full 8 frames a second (150 ms of work per frame down to 20). MOBOTIX frames usually change only a small part of the picture; MxScout now only recolors the parts that changed instead of all 6 million pixels, and on a big tile decodes at half size when that's close to the tile's size.
- Recordings on a NAS load faster: the pieces of each recorded minute are now read several at a time instead of one after another.
- FIX: tooltips on the play controls no longer blink. That bar sits at the bottom of the window, where Windows had no room to show the tooltip below the mouse and put it on top of the pointer instead. Those tooltips now open above the controls.
- View > Show Technical Info on Tiles now also works in Playback: where the recording comes from, how long it took to read, decode time and frames per second - handy to tell a slow network from a slow PC.

## MxScout 1.5.2  (November 8, 2026)
- FIX: scrubbing the timeline. The timeline showed a whole hour, so a short recording was only a few pixels wide and the slightest drag ran off it into empty time (black picture). Now:

## MxScout 1.5.1  (November 8, 2026)
- Scrubbing: dragging the timeline now shows the real moving video, frame by frame, instead of one still picture per minute (and .mxg clips now show pictures while dragging too). It sharpens to full quality the moment you let go.
- Much faster playback: the MxPEG decoder uses the fast libjpeg method to rebuild pictures, decodes straight to the tile's size (a grid tile never needs all 3-6 megapixels), and keeps bookmarks inside each recording so jumping to any moment is quick - in tests jumping inside a recording went from about half a second to 10-30 milliseconds.
- FIX: tooltips no longer blink. The status bar clock, the playback time and the Pending Adoption button were re-arranging their bars every second or so, which made any tooltip on them flicker; the camera list no longer rebuilds itself just to update online dots.

## MxScout 1.5.0  (November 8, 2026)
- NEW: Recording folders are added automatically. Every camera folder in your recording locations shows up in Video Sources by itself: a folder that belongs to one of your cameras is linked to that camera, and the rest (old, replaced or not-yet-added cameras) are added as recordings with a film icon. Add the camera later and its recordings entry merges into it - layouts follow. Removed folders stay removed (Settings > Recordings > Bring Back Removed Recording Folders). Can be switched off in Settings > Recordings.
- NEW: Playback through the camera. When this PC can't open a camera's recording folder - you're on another network, connected only to the camera, or no recording location is set up - the camera itself fetches its recordings from its file server or SD card and sends them over, like MOBOTIX's own software does. Timeline, speeds, Instant Replay and MP4/MXG export all work the same.
- Camera Properties > Playback from: Automatic (folder, else through the camera), Recording folder only, or Through the camera only.
- Camera Logs has a Recordings List tab showing what the camera reports it has recorded.

## MxScout 1.4.1  (November 8, 2026)
- Recording locations set once in Settings now fill in every camera's Recordings folder by themselves - shown in gray in Camera Properties. No more typing it per camera. Click Automatic to go back to this after picking a folder by hand.
- Finds camera folders up to 3 levels inside a recording location, so pointing it at the whole NAS share works.
- Matches cameras more ways: factory IP from the MAC, the camera's IP or name in the folder's .erdinfo, a folder named after the camera's IP, or the camera's name.

## MxScout 1.4.0  (November 8, 2026)
- NEW: Add Recordings, in Scan for Cameras. Add MOBOTIX recording folders or .mxg clip files as video sources, with no live camera needed. Pick a camera's folder (like 10_12_154_52), the share the cameras record to (each camera folder inside becomes a source), a folder of .mxg clips, or individual .mxg files - or just drag them from Windows Explorer onto the list. They show with a film icon, a preview picture and the time they were recorded; tick them and add them to Video Sources or a new layout like any camera.
- Recordings play in Playback with the timeline, speeds, Instant Replay and export to MP4/MXG. Showing only recordings switches to Playback by itself and jumps to their newest recording. Clips are placed on the timeline at the time the camera recorded them.
- Nothing is copied or changed - MxScout reads the files where they are. Right-click a recording > Show Files in Explorer.
- Very short recordings are now always visible on the timeline.

## MxScout 1.3.3  (November 8, 2026)
- CHANGED: Open Camera Interface now opens the camera at its own address (for example http://192.168.1.127). Your browser asks for the camera's login the first time - let it remember it. The "Open in Camera Interface" button in Camera Logs does the same.
- The no-password option is still there as "Open Camera Interface (auto login through MxScout)" for when you want it.

## MxScout 1.3.2  (November 7, 2026)
- FIX: Open Camera Interface (logged in) could drop you out of the logged-in view when the camera's pages or redirects pointed at the camera's own address. MxScout now keeps every page, link and redirect going through its login relay. (The address your browser shows, like 127.0.0.1:61184, is MxScout on your own PC passing you to the camera - that's normal.)
- NEW: Open Camera Interface (camera's own address) - opens the camera the normal way at its real address; the browser asks for the login.

## MxScout 1.3.1  (November 7, 2026)
- Camera Logs reads the camera's System Messages properly: a table with date, time, service, program and message, colored like the camera colors them, and a summary at the top of every problem with a plain-English "What it means" - for example when the camera can't reach the file server it records to.

## MxScout 1.3.0  (November 7, 2026)
- NEW: Camera Events - right-click a camera. Browse the events (alarms) the camera itself has stored, newest first, as thumbnails with date and time. Click one for the big alarm picture and its details, Play the whole event, or save it as MP4 or MXG. Works straight from the camera, with no file server needed.
- NEW: Camera Actions - right-click a camera: Find This Camera (blinks its LEDs for 10 seconds), Speak IP Address, Read Temperature, LEDs and infrared lights on/off, Acknowledge Error, Sync Clock Now, Test Recording Server, Store Settings, Delete System Messages and Reboot (the last two ask first). Plus Save Support Report - the file MOBOTIX support asks for.
- NEW: View Mode for 180/360 degree cameras (Q, D, C, i models): Panorama, Double Panorama, Surround (4 views), Panorama + Focus, Corrected and Picture-in-Picture. The camera renders the view itself, so it looks exactly like MOBOTIX's own software. Remembered per camera.
- Camera Survey reads the camera's settings list correctly.

## MxScout 1.2.0  (November 7, 2026)
- NEW: Adoption, like UniFi. MxScout keeps watching your network (every 3 seconds, plus a full sweep every minute) and lists MOBOTIX cameras it doesn't manage yet - brand-new ones, or ones removed from MxScout - under the yellow "Pending Adoption" button. Adopt them in one click (set the password first if they need one) or Ignore them. Adopted cameras that get a new IP address are followed automatically, and Video Sources shows a green/red Online dot for every camera.
- NEW: Open Camera Interface (logged in) - right-click any camera: its complete web interface opens in your browser already logged in with the login MxScout has. No password to type, every camera feature within reach.
- NEW: Camera Settings - right-click a camera. Every settings section the camera has, as a proper form built from the camera's own descriptions: drop-downs with the camera's own labels, number boxes with the allowed range, and the camera's explanation as the tooltip. Changed fields turn yellow. Apply shows the exact list of changes, saves a backup of the camera's whole configuration first, sends the changes, checks the camera really took them, saves them permanently and tells you if the camera needs a restart.
- NEW: Download Configuration / Restore Configuration (complete camera configuration files), with automatic backups before every change and when a camera is adopted.
- NEW: Camera Logs - right-click a camera: system messages, camera information and the web server log, errors in red and warnings in amber, refreshing every 10 seconds if you like; save to a file or open the page in the camera's interface.

## MxScout 1.1.2  (November 7, 2026)
- Camera Survey (Help menu) now collects everything needed for the coming Camera Settings and Camera Logs windows: the camera's full configuration, every settings section with its labels and choices, and its log/information pages. Read-only - it never changes anything on the camera - and passwords are shown as ***.

## MxScout 1.1.1  (November 7, 2026)
- FIXED: on screens with Windows display scaling (125%, 150%...) the camera picture was drawn too big, cutting off the camera's own text along the edges (name and date at the top, VM/REC status at the bottom). The whole picture now shows.
- The camera-name bar now sits ABOVE the picture instead of over it, so it never hides the camera's own text.

## MxScout 1.1.0  (November 7, 2026)
- NEW: Automatic updates. MxScout checks for a new version when it starts and every 6 hours. When one is ready, a yellow bar appears at the top: click "Update now" and MxScout downloads it, checks it's genuine (size, checksum and version), swaps itself and restarts - your cameras, layouts and settings stay exactly as they were.
- NEW: Help > Check for Updates Now, and Help > What's New (this list).
- You can switch automatic checking off in Settings > Start-up (takes effect immediately).

## MxScout 1.0.1  (November 7, 2026)
- FIXED: boxes and text overlapping on laptops running Windows display scaling at 125%, 150% or 200%. Every window, list column, icon and gap now grows with your display setting.
- FASTER: camera pictures are shrunk to tile size in the background, so the window stays quick with many cameras.
- The navigator panel remembers its width correctly at any display scaling.

## MxScout 1.0.0  (November 7, 2026)
- First release: a video management program for MOBOTIX cameras, laid out like MxControlCenter.
- Scan for Cameras: pick your network(s); cameras appear with status dot, name, IP, MAC, model, firmware, and whether MxScout already knows them; live preview once the password is set; add to Video Sources or straight into a new layout.
- Layouts tree with folders, Video Sources list, drag-and-drop onto the grid, Auto grid or fixed grids, yellow frame on the active camera, full screen, snapshots.
- Live video that automatically uses less network on big grids.
- Playback straight from the cameras' file-server (SMB/CIFS) recordings: all cameras in sync on one timeline, reverse, fast-forward up to 128x, frame-by-frame, instant replay.
- Export to MP4 (YouTube, email, phones) or the original MOBOTIX .MXG evidence copy.
