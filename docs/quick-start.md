---
layout: default
title: Quick Start
nav_order: 3
---

# Quick Start Guide

Want to see Save System Lite in action immediately? Follow this quick guide to set up a testing script and verify saving and loading is working in your project.

---

## 💻 Complete Integration Script
Create a new C# script in your project named `SaveSystemLiteTest.cs` and paste the following code:

```csharp
using UnityEngine;
using DecnetGames.SaveSystemLite;

public class SaveSystemLiteTest : MonoBehaviour
{
    [Header("Testing State")]
    public string playerName = "Adventurer";
    public int currentLevel = 5;
    public Vector3 currentPosition = new Vector3(10f, 1.5f, 20f);
    public Color equipmentColor = Color.cyan;

    private void Update()
    {
        // Press S key to Save
        if (Input.GetKeyDown(KeyCode.S))
        {
            SaveState();
        }

        // Press L key to Load
        if (Input.GetKeyDown(KeyCode.L))
        {
            LoadState();
        }

        // Press D key to Clear/Delete
        if (Input.GetKeyDown(KeyCode.D))
        {
            ClearState();
        }
    }

    private void SaveState()
    {
        // 1. Set our active slot to Slot 0
        SaveSystemLite.SetSlot(0);

        // 2. Save individual keys
        SaveSystemLite.SaveValue("player_name", playerName);
        SaveSystemLite.SaveValue("current_level", currentLevel);
        SaveSystemLite.SaveValue("position", currentPosition);
        SaveSystemLite.SaveValue("eq_color", equipmentColor);

        Debug.Log("[SaveSystemLite] Save complete! Press 'L' to load or inspect the file.");
    }

    private void LoadState()
    {
        SaveSystemLite.SetSlot(0);

        // Load values back, providing default fallbacks if keys don't exist
        playerName = SaveSystemLite.LoadValue<string>("player_name", "New Player");
        currentLevel = SaveSystemLite.LoadValue<int>("current_level", 1);
        currentPosition = SaveSystemLite.LoadValue<Vector3>("position", Vector3.zero);
        equipmentColor = SaveSystemLite.LoadValue<Color>("eq_color", Color.white);

        Debug.Log($"[SaveSystemLite] Loaded! Player: {playerName}, Level: {currentLevel}, Pos: {currentPosition}, Color: {equipmentColor}");
    }

    private void ClearState()
    {
        SaveSystemLite.SetSlot(0);
        SaveSystemLite.DeleteSave();
        Debug.Log("[SaveSystemLite] Deleted slot 0 save file.");
    }
}
```

---

## 🏃 Running the Test

1. Create a new empty GameObject in your scene (e.g. `GameObject > Create Empty`). Name it `SaveTest`.
2. Attach the `SaveSystemLiteTest` script to it.
3. Enter **Play Mode** in the Unity Editor.
4. Modify any fields in the Inspector (e.g., change level to `99` or edit coordinates).
5. Press the **`S`** key on your keyboard. Check the Console to confirm saving.
6. Stop Play Mode, restart Play Mode (all values will return to defaults).
7. Press the **`L`** key on your keyboard. Watch the inspector values restore instantly!

> **Pro Tip**: To verify where files are written, open `Tools > Save System Lite > Control Panel` and click **Open Save Folder**. You will see the `save_slot_0.json` file. Opening it reveals a clean, human-readable structure!
