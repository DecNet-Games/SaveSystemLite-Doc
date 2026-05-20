---
layout: default
title: Multi-Slot Management
parent: Core Features
nav_order: 1
---

# Multi-Slot Management

Most free save engines hardcode data to a single file, forcing developers to build slot management and path tracking entirely from scratch. Save System Lite provides high-performance, slot-aware storage out of the box, supporting three isolated slot files (Slot 0, 1, and 2).

---

## ⚙️ Selecting an Active Slot
At any time, you can query or set the active save slot using the static API. All subsequent saves and loads will automatically apply to this active index:

```csharp
using DecnetGames.SaveSystemLite;

// Set the active slot to Slot 1 (for example, from a menu selection)
SaveSystemLite.SetSlot(1);

// Save level data specifically to Slot 1
SaveSystemLite.SaveValue("level_id", 3);

// Query the currently active slot index
int activeSlot = SaveSystemLite.GetSlot();
Debug.Log($"Current active slot: {activeSlot}"); // Outputs: 1
```

---

## 📂 Target Locations on Disk

Save System Lite maps directories programmatically, avoiding hardcoded paths that break across platforms. The folders match standard Unity guidelines:

*   **Windows / Standalone**: `C:\Users\[Username]\AppData\LocalLow\[CompanyName]\[ProjectName]\SaveSystemLite\save_slot_[Index].json`
*   **macOS**: `~/Library/Application Support/[CompanyName]/[ProjectName]/SaveSystemLite/save_slot_[Index].json`
*   **Android / iOS**: Internal application sandbox folders, isolated and fully secured from standard user tampering.
*   **WebGL**: Uses standard browser HTML5 IndexedDB / LocalStorage, writing under the secure keys: `SaveSystemLite_Data_Slot_[Index]`.

---

## 🧼 Clearing Slots
To reset player profiles or implement a "Delete Save Slot" UI action:

```csharp
// Delete all data stored in the currently active slot
SaveSystemLite.DeleteSave();

// Delete a specific slot directly without changing active selection
SaveSystemLite.DeleteSave(2); // Erases Slot 2 permanently
```

> **Warning**: Deletion is final. When calling `DeleteSave()`, the slot's `.json` file is deleted from disk instantly. Ensure you confirm the choice with an editor or game dialog!
