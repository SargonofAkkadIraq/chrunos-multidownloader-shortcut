# Chrunos Multi Downloader Shortcut

This repository contains a human-readable JSON description of an iPhone Shortcut named "Chrunos Multi Downloader". The Shortcuts app on iPhone does not accept a raw JSON import in most cases — if the direct import of a .shortcut file is required, you can manually recreate the shortcut using the steps below.

Raw JSON description (suitable for manual recreation):
- File: chrunosmultidownloader.shortcut.json

What the shortcut does (summary):
1. GET the JSON at https://raw.githubusercontent.com/CodyChrunos/Shortcuts/refs/heads/main/chrunosmultidownloader.json and parse it into "update".
2. If update.pVersion == 1.1:
   - Prompt to confirm sending the clipboard to the remote API (safety check).
   - POST {"url":"<clipboard>","quality":"720"} to update.api.
   - If API response contains "error": open https://t.me/chrunoss in Safari.
   - Else if response contains "url": download that file and save to Files → Shortcuts/Downloads.
3. Else (pVersion != 1.1): open update.url in Safari.

Default save location on the device: Files → Shortcuts/Downloads

How to install on iPhone (manual recreation):
1. Open Shortcuts app on your iPhone.
2. Tap + to create a new shortcut.
3. Add the following actions in order and configure using the JSON file as a guide:
   - Get Contents of URL (GET) -> URL: https://raw.githubusercontent.com/CodyChrunos/Shortcuts/refs/heads/main/chrunosmultidownloader.json
   - Get Dictionary from Input
   - If (Condition: Dictionary Value for pVersion is 1.1)
       - Ask for Input (Confirm) -> prompt: "Send the current clipboard contents to the remote API?"
       - Get Clipboard
       - If (If result of Ask for Input is true)
           - Get Contents of URL (POST) -> URL: (Magic variable: update.api) Headers: Content-Type: application/json Request Body (JSON): {"url":"(Clipboard)","quality":"720"}
           - Get Dictionary from Input
           - If (Dictionary contains key "error")
               - Open URLs -> https://t.me/chrunoss
             Else
               - If (Dictionary value for url is not empty)
                   - Get Contents of URL (GET) -> URL: (Magic variable: url from response)
                   - Save File -> Service: iCloud Drive, Path: Shortcuts/Downloads (uncheck Ask Where to Save)
   - Otherwise (Else of main If)
       - Open URLs -> (Magic variable: update.url)

If you want a true single-file .shortcut for direct import, reply and I will attempt to generate an exportable .shortcut file and add it to the repo. Note: Shortcuts .shortcut files are binary/plist bundles; directly constructing them may fail without testing on an Apple device.

Raw download link (JSON description):
https://raw.githubusercontent.com/SargonofAkkadIraq/chrunos-multidownloader-shortcut/main/chrunosmultidownloader.shortcut.json

