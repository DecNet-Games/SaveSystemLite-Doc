---
layout: default
title: Getting Started
nav_order: 1
---

# Getting Started

Getting started with **Save System Lite** takes less than a minute. This page covers the core concepts, namespaces, and standard architectures of the system.

---

## 🏛️ Core Concepts

Before writing save and load logic, it's helpful to understand the underlying framework:
1. **The Active Slot**: Save System Lite runs on an active slot indexing system (Slot 0, 1, or 2). All save and load operations will query this selected active slot unless specified otherwise.
2. **Whole-Object Serialization**: You can pass any standard C# class containing player data directly to `SaveSystemLite.Save()`. The engine serializes the entire object to a single file.
3. **Key-Value Variable Database**: Alternatively, you can save and load individual variables directly under unique string keys (e.g., `SaveValue("high_score", 500)`). The system handles the backing key-value slot dictionary automatically.

---

## 🛠️ Step 1: Using the Namespace
To use the Save System Lite API, add the namespace declaration at the top of your C# scripts:
```csharp
using DecnetGames.SaveSystemLite;
```

---

## 🛠️ Step 2: Slot Selection
Select the active save slot when your player loads their profile or selects a slot from a save/load menu:
```csharp
// Set active slot to Slot 1
SaveSystemLite.SetSlot(1);
```

---

## 🛠️ Step 3: Performing a Save Operation
You can serialize a full class object, or update specific variables in the database.

### Method A: Saving a Class Object
```csharp
[System.Serializable]
public class GameSaveData
{
    public int goldAmount;
    public string currentStage;
}

// In your game controller:
GameSaveData myData = new GameSaveData { goldAmount = 100, currentStage = "Chapter 1" };
bool success = SaveSystemLite.Save(myData);
```

### Method B: Saving Key-Values
```csharp
SaveSystemLite.SaveValue("player_health", 85f);
SaveSystemLite.SaveValue("player_color", Color.yellow);
```

---

## 🛠️ Step 4: Loading Saved Data
To restore data at startup or scene transitions:

### Loading a Class Object
```csharp
GameSaveData myData = SaveSystemLite.Load<GameSaveData>();
if (myData != null)
{
    Debug.Log($"Restored! Gold: {myData.goldAmount}");
}
```

### Loading Key-Values
```csharp
float health = SaveSystemLite.LoadValue<float>("player_health", 100f); // Default to 100f if key missing
Color playerColor = SaveSystemLite.LoadValue<Color>("player_color", Color.white);
```

---

> **Pro Tip**: To inspect what is being written to disk in real-time, keep the `Tools > Save System Lite > Save Inspector` window open while running your game in the editor!
