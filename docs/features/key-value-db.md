---
layout: default
title: Key-Value Database
parent: Core Features
nav_order: 2
---

# Key-Value Database Layer

Save System Lite contains an integrated **Key-Value database layer** that runs inside each save slot. This allows you to write individual variables dynamically, rather than rewriting a massive C# class representation every time a single value changes.

---

## 🚀 Overcoming Unity's JSON Utility Limits
Unity's built-in `JsonUtility` is fast, but it is notoriously limited. It **fails** to serialize basic Unity struct objects like `Vector3`, `Quaternion`, or `Color` directly, either returning empty objects or throwing severe runtime exceptions.

To bypass this without forcing you to import bulky external DLLs (like Newtonsoft.Json) that crash user installations, we built **custom lightweight wrappers** directly into the engine backend. They automatically convert structures behind the scenes:

*   **`Vector3`** $\rightarrow$ wrapped and converted to coordinates dynamically.
*   **`Quaternion`** $\rightarrow$ Euler rotation converted and stored smoothly.
*   **`Color`** $\rightarrow$ Red, Green, Blue, Alpha floats structured cleanly.

---

## 📝 Writing Variables to the DB
To write values into the database, use `SaveValue()`:

```csharp
using DecnetGames.SaveSystemLite;
using UnityEngine;

// Save an integer
SaveSystemLite.SaveValue("player_gems", 250);

// Save a string
SaveSystemLite.SaveValue("quest_active", "TheLostRelic");

// Save a Vector3 (normally crashes other serializers)
SaveSystemLite.SaveValue("spawn_coordinates", new Vector3(45.5f, 10.2f, -12.1f));

// Save a Color
SaveSystemLite.SaveValue("custom_banner_color", Color.magenta);
```

---

## 🔍 Reading Variables from the DB
To read values, use `LoadValue<T>()`. You must provide a **default fallback value** which the method returns if the key does not exist yet (e.g. at the first launch of the game):

```csharp
// Load an integer, defaulting to 0 if not found
int gems = SaveSystemLite.LoadValue<int>("player_gems", 0);

// Load a Vector3, defaulting to Vector3.zero
Vector3 spawn = SaveSystemLite.LoadValue<Vector3>("spawn_coordinates", Vector3.zero);

// Load a Color, defaulting to Color.white
Color banner = SaveSystemLite.LoadValue<Color>("custom_banner_color", Color.white);
```

---

## ❓ Checking Key Existence
Before attempting to load or perform runtime game setups, you can verify if a specific variable key exists:

```csharp
if (SaveSystemLite.KeyExists("spawn_coordinates"))
{
    // Apply coordinates safely
    transform.position = SaveSystemLite.LoadValue<Vector3>("spawn_coordinates");
}
else
{
    // Execute default spawn sequence
    transform.position = defaultSpawnAnchor.position;
}
```
