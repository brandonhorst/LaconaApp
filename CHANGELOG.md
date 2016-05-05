# Public Beta 8 (0.7.0)

## New Features

- Added the "open Lacona Preferences" command (this does the same thing as CMD+,)
- Added support for "qualifiers" - a way of unambiguously specifying ambiguous commands. Try the `call` command for a contact with multiple phone numbers.
- The `open` command can now open Contacts, which will open in the Contacts application

## Fixes

- Fix a bug where entering an empty string on the settings page could revert data to the defaults
- Fix a bug where "search <engine> for <query>" was not ignoring the word "for"
- Fix two separate bugs that resulted in certain commands were not presenting all available options
- Relationship-Name linking was made much more robust, so it now accepts names with spaces in them
- You can no longer open multiple preference panes with a single command (which never worked to begin with)

## Changes

- Improve text rendering quality on some systems

# Public Beta 7 (0.6)

## New Features

- Added the ability to start Facetime Audio calls

## Fixes

- Do not hijack modifier+arrow key combinations (like Command+Left)
- Changes to Applications settings will now take effect immediately
- Fix a bug with opening "~/*" files
- Fix a crash when typing quotation marks

## Changes

- Reworked everything under-the-hood using [elliptical](http://elliptical.laconalabs.com/), for improved performance and (future) extensibility
- Cleaned up the language for making calls, texts, emails, facetime calls, and facetime audio calls
- Changed the colorization of "time of day" and "folder"
- Due to under-the-hood changes, nothing works when running outside of the Applications directory

# Public Beta 6 (0.5)

## New Features

- Added the Lacona Preferences Page
- Added the ability to manage the list of directories to search for applications
- Added the ability to customize Lacona's search engines
- Added the ability to hide the menubar icon
- While Lacona is open, pressing Command+q quits it
- While Lacona is open, pressing Command+, now opens the Preferences

## Fixes

- Fix a bug where iTunes songs missing some info could result in 'play undefined' being a valid command
- Fix a bug where using a quotation mark in an "open" command would crash Lacona
- Allow Lacona to find files whose names have diacritical marks in them
- "schedule x next Friday to Sunday" would previously fail
- Fix a bug which could cause crashes on startup if launched outside /Applications more than once
- Fix a bug that would result in executing the wrong command if the user typed and pressed enter very quickly
- Removed some unnecessary files from Resources

---

# Public Beta 5 (0.4.2)

## Fixes

- Fixed a bug where "open lacona.io and <...>" would sort before "open lacona.io"
- Reverted a broken implementation of "call/email/text/facetime" to 0.4 version

---

# Public Beta 4 (0.4.1)

## Fixes

- Lacona would previously ignore some applications/bookmarks if you had more than 100
- In version 0.4, Lacona could not open Apps/Pref Panes/Volumes and Files/URLs in the same command - now it can again
- Auto-update library (Sparkle) updated to version 1.13.1, to fix [a recently-discovered security vulnerability](https://github.com/sparkle-project/Sparkle/releases/tag/1.13.1).

## Changes

- If running outside of the Applications directory, Lacona will ask to move itself. Outside of the Applications directory, OSX does not allow apps to access Contacts, Calendar, etc...
- Lacona now differentiates between "files" and "folders".
- Lacona can now open Applications that live outside the /Applications directory. To limit clutter, it is limited to these directories: 
  * `/Applications` - System, App Store, and normal Apps
  * `/Applications/Xcode.app/Contents/Applications` - Developer utilities, if Xcode is installed
  * `/System/Library/CoreServices/Applications` - System utilities
  * `~/Applications` - Chrome Apps, among other things
  * `/usr/local/Cellar` - Apps installed via Homebrew
  * `/opt/homebrew-cask/Caskroom` - Apps installed via Homebrew Cask
  * `Finder.app`
- In the "open" command, Applications and Preference panes will always appear above files, even if the beginning of the name is not matched.
- File searching performance improved dramatically.

---

# Public Beta 3 (0.4)

## New Features

- Added the "schedule" command - you can now schedule events on the default calendar using natural language
- You can now open files by name, just like a Spotlight search
- You can now open files by entering a file path

## Changes

- Fallthroughs are now displayed without a border, to reduce visual complexity
- Lacona will now appear on the active display, rather than always the first one
- Lacona will now display lower on most screens (centered vertically, if there were 9 rows of data displayed)
- If you are setting an F-key as the Keyboard Shortcut, you do not need to use a modifier (though you still may)
- The "search <query> on <engine>" command now sorts above the "open <url>" command, to make fallthrough searching slightly easier.
- Command continuation information (in repeats and sequences) is not displayed for complete outputs. Use `{Right}` or `{Tab}` to see continuations

## Fixes

- Lacona will now resize automatically if the display size changes
- The "shutdown" command is now functional
- The "eject all" command is now functional
- Plug a memory leak with Spotlight queries

---

# Public Beta 2 (0.3.1)

## New Features

- Allow Lacona to control Light/Dark mode ("enable dark mode", "toggle light mode"...)
- Add 3 new themes (light, light-minimal, and dark-minimal)
- The Lacona theme can be set to automatically mirror the OS theme (light/dark mode)
- Switched to "One" color scheme, based on Atom One, for improved light-mode visibility
- Allow vim-style (hjkl) movement when holding the control key
- Added an About panel

## Changes

- Thin down the status menu icon a bit
- Lacona width is now limited to 820px maximum, to help people with large screens
- Even up the space between fallthroughs and the rest of the words

## Fixes

- Prevent "rubber band" effect that moves the entire Lacona window when scrolling past edges
- Fix a bug where Lacona could be displayed but not focused
- Prevent Lacona from stealing the current App's focus
- Ensure that "tonight" in "remind me to eat tonight" is properly colorized
- Lacona refuses to launch on OSX <= 10.10

---

# Public Beta 1 (0.3)

- Initial Beta Launch
