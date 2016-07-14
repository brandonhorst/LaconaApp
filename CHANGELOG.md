# Public Beta 12 (0.10.0)

## New Features

- Add the ability to download and install addons published to npm. Check out the [documentation for writing your own addons!](https://docs.lacona.io).
- Introduce small icons for certain features (Apps, Contacts, Bookmarks, Preference Panes, Contacts)
- Add the Calculate command, which can do basic arithmetic and unit conversions. For a list of features, see [MathJS](http://mathjs.org/). Results appear in a popover window.
- Add the Define command, which looks up words in the system dictionary. Currently, only the Oxford English Dictionary is supported.
- Add commands to Move, Delete, Copy, and Reveal files and folders (thank you to @rltbennett)
- Added a fallthrough for Calculate
- You can now open Apps using some common alternative names (e.g. Chrome -> Google Chrome, iMessage -> Messages). If there are more apps with alternative names that are not supported, please [submit an issue](https://github.com/laconalabs/LaconaApp/issues).
- Introduce the ability to open Volumes
- Add qualifiers to relationships, both by label (my brother (Mobile)) and by name (my brother (Aaron))
- Add a small introductory popover on first launch, explaining how to open the Lacona bar and preferences
- Opening Lacona from Finder or the Dock will now bring up the Lacona bar
- You can now toggle multiple settings with the same command ("turn off wifi and bluetooth")
- The Mute and Do Not Disturb commands now support a time duration ("mute for 10 minutes")

## Changes

- Switch the underlying API to use Node.js instead of JavascriptCore. Improved performance for all commands. May require addon changes.
- Switched `lacona-api` to use Promises and Observables more consistently - may require addon changes.
- Updated the underlying elliptical engine, which has a few minor changes to better support qualifiers and annotations. May require addon changes.
- Shrank the text and simplified the visual style to allow popover previews and icons to better fit with the flow of content
- The Keyboard Shortcut can no longer be set to to Shift+[Letter/Number/Punctuation], as those are normal typing characters. 
- Add a brief description to the Keyboard Shortcut setting
- Change the Preferences styling to fit more in line with OSX
- Remove the Right Click menu from Preferences and Lacona Options
- Changed the way that Preferences are saved on disk
- Switched to using Service Management for Launch at Login functionality

## Fixes

- Fix a crash when adding an invalid Application name to Applications
- Fix a bug when attempting to remove certain settings that have defaults.
- Relationships will now work even if the name has diacritical marks.

# Public Beta 11 (0.9.0)

## New Features

- Lacona can now quit menu bar apps
- Added the `relaunch` command (works with Dock and Menu Bar apps)
- API: Addons can now use `callNode` to make calls out to Node js, where they can use Node modules like `fs` and `https`.

## Changes

- Show all entries for certain commands before any characters have been input (eject, switch to, quit)
- Add `activate` as a synonym for `switch to`
- Enable fuzzy matching for many more commands
- Visual: Slightly decrease shadow
- API: Split File and Directory into two distinct phrases (rather than File encompassing both)
- API: RunningApplication results have a new property: `activiationPolicy`, either "regular", "accessory", or "prohibited"

## Fixes

- Fix a bug that could clear command settings with every relaunch
- Fix a bug where RunningApplications, Contacts, and Volumes would not be updated if they changed after Lacona launch
- API: Fix a bug with `quitApplication` not calling the callback

# Public Beta 10 (0.8.1)

## Fixes

- Fix a bug that would cause silent failures if the user had never used Lacona before

# Public Beta 9 (0.8.0)

## New Features

- Add limited support for developer addons
- Add the "reload addons" Applescript command

## Fixes

- Fix a bug with "toggle Do Not Disturb"
- Fix a display bug visible on Retina displays

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
