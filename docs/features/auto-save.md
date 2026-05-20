---
layout: default
title: Lite Auto-Save Component
parent: Core Features
nav_order: 3
---

# Lite Auto-Save Component

Writing scripts to track coordinates and rotation values on every moving item in a level can be tedious. Save System Lite provides a zero-code solution for automated state saving: **`SaveSystemLiteAutoSave`**.

---

## 🤖 What does it track?
This lightweight drag-and-drop component integrates with the Key-Value database backend. It automatically tracks:
*   **GameObject Position (`Vector3`)**
*   **GameObject Rotation (`Quaternion`)**

---

## ⚙️ Drag-and-Drop Setup

To automate any object's transform:
1. Select the GameObject in your Unity hierarchy (e.g., player, moving platform, checkpoint chest).
2. Click **Add Component** in the Inspector.
3. Search for **`SaveSystemLiteAutoSave`** and select it.
4. Set a unique, descriptive **Save Key** (e.g., `chest_gold_room_0`). 

> **Important**: Every Auto-Save component in your scene must have a completely unique key. If two objects share a key, their save data will override each other, causing visual glitches.

---

## 🔄 Automatic Lifecycle Management
The script takes advantage of Unity lifecycle triggers to save and load data automatically without your intervention:

*   **`Start()` / Awake**: The script automatically queries the active slot database, checks for matching position and rotation keys, and snaps the object back to its saved coordinates.
*   **`OnDisable()`**: Saves the object coordinates instantly when the object is deactivated, hidden, or transitioning.
*   **`OnApplicationQuit()`**: Restores and writes the final transform state immediately before the game client terminates, protecting against data loss.

---

## 🔬 Custom Inspector Options
In the Unity inspector, you can disable specific tracking parameters to fit your gameplay logic:

*   **`Save Position`**: Toggle on/off to enable/disable coordinate tracking.
*   **`Save Rotation`**: Toggle on/off to enable/disable rotation angles.

For example, a moving platform only needs its `Save Position` checked, whereas an interactive spinning camera anchor might only need its `Save Rotation` tracked.
