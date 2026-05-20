---
layout: default
title: Home (Getting Started)
nav_order: 1
---

# Save System Lite Documentation

Welcome to the official developer documentation for **Save System Lite** — the robust, zero-dependency, and incredibly lightweight multi-slot key-value local storage framework for Unity.

Are you tired of raw JSON serializers throwing compile errors, failing on simple Unity structural types like `Vector3`, `Quaternion`, and `Color`, or forcing you to write tedious slot boilerplate code? Save System Lite solves these challenges instantly. It provides an elegant, optimized Key-Value database layer that gives you local file structure, slot management, and auto-saving in a tiny, high-performance runtime package.

---

## ⚡ Key Features

*   **Multi-Slotting out of the Box**: Support for `Slot 0`, `Slot 1`, and `Slot 2` natively using a single static method call.
*   **Slot-Aware Key-Value Storage**: Store individual variable states under custom keys within specific slot files. No more full file parses just to read a single integer.
*   **Native Unity Structure Serialization**: Built-in support to serialize and deserialize complex Unity types like `Vector3`, `Quaternion`, and `Color` without raw JSON crashes or external dependencies.
*   **Drag-and-Drop Auto-Save Component**: Free-tier script to automatically track and restore object position and rotation on quit or disable.
*   **Editor Control Center & Inspector**: A gorgeous, dark-themed control center featuring one-click integration guides, slot management, and raw JSON editor windows directly inside the Unity IDE.

---

## 🚀 Pain vs Solution

| The Pain (Standard JSON / Other Free Assets) | The Solution (Save System Lite) |
| :--- | :--- |
| Handcrafting Slot I/O, folder directories, and platform-specific code takes hours. | **Multi-Slot support is instant.** Zero configuration, fully managed local slot directories. |
| Unity primitives (`Vector3`, `Color`) cannot be serialized natively, causing crashes. | **Built-in wrappers** seamlessly handle basic Unity structures automatically. |
| Restoring object state manually requires complex managers and tedious event rigging. | **Drag-and-drop auto-save** handles object transform states on application shutdown. |
| Looking inside save files requires opening deep local folders and manual Notepad edits. | **Built-in Visual Inspector** lets you read, edit, and delete slot keys inside Unity. |

---

## 🛠️ Quick-Start Integration (1 Minute)

```csharp
using UnityEngine;
using DecnetGames.SaveSystemLite;

public class LiteQuickStart : MonoBehaviour
{
    private void Start()
    {
        // 1. Set the active slot (0, 1, or 2)
        SaveSystemLite.SetSlot(0);

        // 2. Save dynamic variables to the key-value database
        SaveSystemLite.SaveValue("player_health", 95f);
        SaveSystemLite.SaveValue("spawn_point", new Vector3(10f, 2f, -5f));

        // 3. Load variables safely with custom fallback defaults
        float health = SaveSystemLite.LoadValue<float>("player_health", 100f);
        Vector3 spawn = SaveSystemLite.LoadValue<Vector3>("spawn_point", Vector3.zero);

        Debug.Log($"Loaded Player State: Health={health}, Spawn={spawn}");
    }
}
```

> **Pro Tip**: Under the hood, Save System Lite handles paths automatically. On Standalone platforms (Windows/Mac/Linux), it writes to `Application.persistentDataPath/SaveSystemLite/`, while on WebGL it automatically fallbacks to HTML5 LocalStorage via high-performance `PlayerPrefs` wrappers, ensuring your game compiles and works anywhere with zero edits!

---

## 📖 Explore the Documentation

Start building your save integration by navigating through the resources below:

*   [**Installation Guide**](docs/installation.html)
*   [**Quick-Start Guide**](docs/quick-start.html)
*   [**Core Features Deep-Dive**](docs/features/index.html)
    *   [Multi-Slot Management](docs/features/slots.html)
    *   [Key-Value Database](docs/features/key-value-db.html)
    *   [Lite Auto-Save Component](docs/features/auto-save.html)
*   [**Frequently Asked Questions (FAQ)**](docs/faq.html)
