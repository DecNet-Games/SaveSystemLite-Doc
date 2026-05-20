---
layout: default
title: FAQ
nav_order: 5
---

# Frequently Asked Questions (FAQ)

Here are the most common questions developers ask when integrating and using **Save System Lite**.

---

## ❓ 1. Can I increase the slot limit from 3?
No. Save System Lite is hardcoded to support 3 slots (`Slot 0`, `Slot 1`, `Slot 2`) to maintain a clean, lightweight memory footprint. If your game requires 99 save slots, dynamic name tags, slot playtime counters, last-saved date trackers, or slot cloning, please upgrade to **Save System Pro**.

---

## ❓ 2. How are saves handled on WebGL builds?
When compiling to WebGL, standard file system input-output operations are blocked by browser sandboxes. Save System Lite detects this environment automatically at compile-time:
*   On standalone platforms, it writes clean `.json` files.
*   On WebGL, it seamlessly maps data into the browser's HTML5 LocalStorage via high-performance `PlayerPrefs` wrappers.

You do not need to write a single line of WebGL-specific fallback code!

---

## ❓ 3. Can I serialize dynamic C# Dictionaries or Lists?
No. Standard `JsonUtility` used in Save System Lite does not support dynamic collections (like `Dictionary<string, int>` or nested multi-dimensional lists) out of the box. Attempting to pass them will result in blank objects. 

If your game requires custom collection serialization, upgrading to **Save System Pro** will unlock our pure C# `AdvancedSerializer` engine, which handles Lists, Arrays, and Dictionaries without external DLL dependencies!

---

## ❓ 4. Where can I find the saved files?
You can easily find the directory by opening `Tools > Save System Lite > Control Panel` in the Unity Editor and clicking the **Open Save Folder** button. It will open standard Windows Explorer or macOS Finder pointing directly to the application's persistent sandboxed directory.

---

## ❓ 5. How can I protect files from player editing?
Save System Lite does not encrypt files, meaning they are stored as raw JSON to allow easy developer debugging. 

If your game features leaderboard mechanics, in-app purchases, or multiplayer integration and you need to protect files from player editing, **Save System Pro** includes native **AES-128 Military Grade Encryption** and **Anti-Corruption Backups (.bak file protection)**, securing files from local cheat tools.
