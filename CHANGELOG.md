# MxScout - Release Notes

## MxScout 1.5.4  (November 8, 2026)
- FIX: fast forward and rewind at 16x and above showed "No preview available". At those speeds MxScout used to show each recorded minute's small preview picture (INFO.jpg), which many cameras fill with that placeholder. It now shows the real video, smaller and skipping frames so it keeps up. Placeholder pictures are ignored everywhere (Add Recordings preview, Live-mode stills too).

## MxScout 1.5.3  (November 8, 2026)
- FASTER PLAYBACK of big cameras. Measured on a 6-megapixel recording: a large single-camera tile went from about 6 to the full 8 frames a second (150 ms of work per frame down to 20). MOBOTIX frames usually change only a small part of the picture; MxScout now only recolours the parts that changed instead of all 6 million pixels, and on a big tile decodes at half size when that's close to the tile's size.
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
- Recording locations set once in Settings now fill in every camera's Recordings folder by themselves - shown in grey in Camera Properties. No more typing it per camera. Click Automatic to go back to this after picking a folder by hand.
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
- Camera Logs reads the camera's System Messages properly: a table with date, time, service, program and message, coloured like the camera colours them, and a summary at the top of every problem with a plain-English "What it means" - for example when the camera can't reach the file server it records to.

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
