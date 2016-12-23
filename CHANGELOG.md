# 1.1.3

## Changes

- "Launch at Login" is no longer be enabled by default, to comply with [Setapp](https://setapp.com/) guidelines. Users who have already set the setting manually will not be affected

## Fixes

- Fix a bug that prevented Launch at Login from working
- Fix a bug that could cause slowdowns if Spotlight returns inconsistent results
- Fix a bug that caused share sheets to appear in the wrong place on Retina displays
- Update the About text to reflect the switch to node v7.0.0

# 1.1.2

## Fixes

- Fix a bug that would reset certain preferences on startup, for users upgrading from Lacona 1.0.x
- Fix a bug that could cause the "Tutorial" popover to not appear on first launch
- Fix the ordering of dialogs presented to the user on first launch

# 1.1.1

## Fixes

- Fix a bug that only allowed one "Shortcut" to be changed from the default at a time.

# 1.1.0

## New Features

- Major revamp of Preferences. Icons make things look better, and all addons and built-in commands show Examples of how they are used. Revamped the License page, added tabs, and array preferences now show up in sheets.
- Added the ability to conditionally enable built-in features via Preferences. Disabling features that you do not need may improve performance.
- Added "Context" support - Lacona is now aware of the current clipboard contents, and the current Finder window (if it is foremost). This means that commands like "email clipboard contents to Vicky" are now possible. Or, with the `lacona-shell` Addon, "run rm -rf * in {current finder directory} is now very easy". This works for URLs, Files, Directories, and text on the clipboard. This can be disabled from 'macOS Integration' in Preferences.
- You can now now specify your "Quick Select Modifier", which allows you to select which modifier key you use to pick an option by number. Previously, it was always set to `alt`.
- Added a one-time popup prompting for Contacts, Reminders, and Events access. If the user clicks no, the functions will automatically be disabled in settings.
- If Contacts, Reminders, and Events access are not permitted, they will automatically be disabled in the Preferences as well.
- The 'reveal in Finder' command can now reveal Applications and Volumes (not just files).
- You can now install Addons by clicking a link from any application. Links in the form [`lacona-install://lacona-convert-currency`](lacona-install://lacona-convert-currency) will pop up an alert asking you to confirm installation. If confirmed, the Addon will automatically install. This only works for published Lacona Addons.
- Check out the "GitHub" and "IFTTT" addons!

## Changes

- Massive performance improvements, especially for users who have a lot of Contacts. On our test system, performance for the `open` command and all fallthroughs was increased about eightfold.
- Fetch some data at load time, increasing performance the very first time Lacona is called up after a restart.
- Small change to the way that Command Aliases work. If the alias matches the input exactly, the full replacement will be used. Now, you can shorten long, commonly used commands that do not require arguments, such as "open twitter.com in Safari".
- Lacona now understands 24-hour time.
- Lacona now understands dates like "July 4-5", "3-5pm", and "the 25th".
- Lacona now makes its understanding of dates a bit more explicit, by automatically adding components like "at", "on", and ":00".
- Whack 17MB off the application size with minification/deduplication. Note that the majority of the large file size comes from bundling Node.js, which is required for functioning.
- IPC with the Node process no longer goes through the network adaptor. This improves performance, and also remove the annoying "Allow Incoming Connections" message that occassionally appeared on Startup.
- Add some attributions to the About page.
- "Play next song" and kin are now properly identified as symbols.
- Songs in iTunes shows the iTunes logo.
- Safari bookmarks now use the Safari logo
- Do not show duplicate options that represent the same thing ('open Chrome' and 'open Google Chrome')
- Prevent some nonsense inputs ('open Google Chrome and Chrome')

## Fixes

- The "Please Purchase Lacona Pro" popup and the tutorial popup will now both appear even if the Menu Bar Icon is hidden.
- Fix a bug that was causing the "Please Purchase Lacona" popup/delay to happen for some system commands.
- Fix "enable/disable Dark Mode" on OSX Sierra
- Selecting options using the mouse now works all the time. Due to an macOS Quirk, this has the unfortunate side-effect of making the cursor always be the normal (rather than having the text and pointer cursors). Not a huge problem, though.

## Developer Changes

- Update underlying node.js to v7.0.0
- Botched addons will no longer break everything. Addons with errors in user-defined code will simply print messages to the log file and Lacona will continue behaving as normal. If your addon is not working, try running `lacona logs`.
- Preferences are now stored in `preferences.json` rather than `config.json`, and they should not include a top wrapper object. This is because preferences are now Addon-specific (Addons cannot access other Addon's config).
- The `auth` type was added to preferences, allowing oauth2-based authentication, straight from Preferences.
- Addons can now specify `examples` in the `lacona` property of `package.json`.
- Addons can now set their own preferences programmatically using the `setConfig` function.
- Addons can now export a `hooks` object, which contains functions that are called at various times. Currently, the `onLoad`, `onLoadConfig`, and `onURLCommand` hooks are available. The latter two hooks are passed `observe`, `config`, and `setConfig`, so they can prefetch sources, modify config settings, and respond to URL commands if necessary.
- Beefed up `setClipboard` and `fetchClipboard` - they can now handle files, URLs, and multiple strings.
- The `image` type is now available for annotations, allowing Addons to specify annotations with an absolute file path to an image file.
- The `url` type is now available for annotations, allowing Addons to specify annotations with an http[s] path to an image file.
- Introduced the `symbol` category, which italicizes the words. This demonstrates to the user that the given input is a symbol of some sort.

# 1.0.3

## Changes

- Lacona will now appear in the Dock while the Preferences window is open, allowing for improved window management.
- Clicking the Dock icon while the Preferences window is open will no longer make the Lacona Input Bar appear.
- "search google for lacona" will now present one option instead of two.

## Fixes

- Fix a bug where pressing "Purchase Lacona..." while the purchase sheet was already active would cause bad behavior and crashes.

## Developer Changes

- Introduced `fetchUserDefaults` to `lacona-api`
- Addons can now extend the `elliptical-*` classes, so extensions can now provide Dates, URLs, Email Addresses, Strings, and more.

# 1.0.2

## Changes

- `lacona-cli@1.1.0` adds the concept of "Developer Mode". Using `lacona dev package-name`, you can set a single addon to be in "Developer Mode", which means that the delay and license prompt will not happen, even for unlicensed users. This will make addon development a bit easier for people seeking scholarships.
- Built-in Commands and Addons can now be [translated](http://docs.lacona.io/docs/advanced/translation.html) (no translations are currently available, but they will come with time)
- If any of the built-in commands are installed using [`lacona-cli`](https://www.npmjs.com/package/lacona-cli), that will supercede the built-in version. This allows developers to test fixes and translations of these commands. The built-in commands are
  - [lacona-calculate](https://github.com/laconalabs/lacona-calculate)
  - [lacona-command](https://github.com/laconalabs/lacona-command)
  - [lacona-communicate](https://github.com/laconalabs/lacona-communicate)
  - [lacona-events](https://github.com/laconalabs/lacona-events)
  - [lacona-finder](https://github.com/laconalabs/lacona-finder)
  - [lacona-itunes](https://github.com/laconalabs/lacona-itunes)
  - [lacona-osx](https://github.com/laconalabs/lacona-osx)
  - [lacona-search-internet](https://github.com/laconalabs/lacona-search-internet)
  - [lacona-settings](https://github.com/laconalabs/lacona-settings)
  - [lacona-translate](https://github.com/laconalabs/lacona-translate)

## Fixes

- Fix a bug with pressing the down arrow to navigate lists in the Preferences
- Fix a bug where multiple lists could be selected at the same time in the Preferences

# 1.0.1

## New Features

- Add a small activity indicator to the Addons page

## Changes

- Minor text changes

## Fixes

- Make the Preferences page functional on macOS 10.12 Sierra

# 1.0.0

## New Features

- Payment is now enabled. All built-in commands are free to use forever. Running commands from Addons will have a slight delay and prompt for purchase. Once purchase has been validated, these messages will go away.
- Add the "Shortcuts" section to config, which allows two new feature: Aliases and Prefixes.
    - Aliases are user-defined ways to cut down on typing. They are replacements that can replace either the beginning of commands ('o safari' -> 'open safari') or entire commands ('twifi' -> 'toggle wifi for 1 second')
    - Prefixes have always existed - they are the commands that are selected by default if you do not enter a verb ('safari' -> 'open safari'). Now, they are user-configurable. There are 4 by default: 'open', 'search', 'look up', and 'calculate'.
- Add "Large Fonts" theme, which increases the font size (to pre-0.10.0 size). Very useful on large monitors
- You can now specify a Reminder List for the "remind me to" command, and a Calendar for the "schedule" command. Additionally, added the alternate "add milk to shopping list" syntax, which is a synonym for "remind me to".

## Changes

- Dramatic performance improvements across the board, especially for fallthrough, files, and dates
- Style changes and continued simplifications, to better fit into the larger macOS environment
- Calculate now does math asyncronously, which improves fallthrough performance, especially for searching.
- Add links to the [Terms of Use](https://www.lacona.io/terms) and [Privacy Policy](https://www.lacona.io/privacy) to the About page.
- Ignore starting spaces and multiple spaces
- "Define" is now only available for dictionary words - it will not do automatic truncation/adjustment
- "Look up" is now a synonym for "define"
- Add "look up" as a fallthrough (user-configurable)
- Applications now have qualifiers, which fixes problems if you have multiple applications in different directories with the same name
- Allow the word form of numbers to be used in dates ("remind me to eat in an hour", "schedule party for march first")
- Increase the transparency of inactive modifiers in the Keyboard Shortcut setting
- "Eject <Volume>" and "eject all" will now show a notification on success or failure
- Change the color of the "reminder title" argument, so it does not blend in with dates and times
- Hide the "disable/enable" button while uninstalling addons.
- Scheduling all-day events now creates an alarm at 9am the day before the event, rather than 11:45pm the day before.
- Make the initial tutorial popover less ugly.

## Fixes

- Fix a bug that could cause options and the preview popover to become invisble, but their shadow to persist
- Fix "open Lacona Preferences"
- Reminders created with lacona will now display their due date in the iOS Reminders App
- Fix a bug that did not allow "schedule x from today to tomorrow"
- Force Lacona's built-in NPM tool to use `~/.lacona-npm` as the cache directory, rather than the default `~/.npm`. This fixes some situations where pre-existing npm permissions issues could cause Addon installation/uninstallation failures for Lacona. Also, prevent other undesired interactions with npm config files.
- Fix a potential crash when editing theme settings for the first time.
- Fix a regression that ignored the "Applications" setting - so default setting users could not open Finder.

# Public Beta 13 (0.10.1)

## Fixes

- Fix a bug that could cause crashes if some running applications did not have bundle identifiers
- Fix a bug with activating and quitting running applications with whitespace in their titles
- The lacona addon log will now be appended to rather than overwritten with each error, making addon development easier
- Fix the `lock computer` command
- Ensure that the website link appears for addons that are not yet installed
- Ensure that author name appears for addons that have been installed
- Fix a bug that could result in Lacona not launching properly if certain Network devices were disabled or the hosts file was configured strangely
- Installation and Uninstallation failures will now be reported as alerts, so there is no need to search through the console logs
- The "Check for Updates" button on the Addons will be re-enabled if errors occur
- Fix a crash that could occur if attempting to install multiple addons at the same time
- Fix an issue that could get an node_modules into an inconsistent state if multiple addons were installed and uninstalled at the same time
- Vertically center the keyboard hints on the right side of options, could potentially fix a display bug on some external monitors

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
