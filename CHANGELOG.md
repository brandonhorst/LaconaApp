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
