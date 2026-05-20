---
layout: default
title: Installation
nav_order: 2
---

# Installation Guide

To ensure proper licensing, support, and access to automatic updates, **Save System Lite** must be acquired officially via the Unity Asset Store. Do not import raw files from unauthorized third-party git registries.

---

## 🛠️ Step 1: Add to Your Assets
1. Open the [Unity Asset Store](https://assetstore.unity.com/) in your web browser.
2. Search for **Save System Lite - DecNet Games** (or click your purchase link).
3. Click **Add to My Assets**.

---

## 📥 Step 2: Download & Import in Unity
1. In the Unity Editor, open the **Package Manager** (`Window > Package Manager`).
2. Change the package filter dropdown in the top-left to **My Assets**.
3. Locate **Save System Lite** in your list of assets.
4. Click **Download** in the bottom-right corner.
5. Once downloaded, click **Import**.
6. In the Import Unity Package window, keep all files checked and click **Import** to merge the folder into your `Assets/SaveSystemLite` directory.

---

## 🏗️ Step 3: Welcome & Verification
Once the import completes, Save System Lite will automatically compile and run a startup script to verify everything is integrated:
1. In Unity, go to the top menu and select `Tools > Save System Lite > Welcome & Setup`.
2. A beautiful, dark-blue welcome panel will appear, greeting you.
3. Click the **Open Lite Control Panel** button to launch your management dashboard.
4. Click **Generate Lite Interactive Demo Scene** to instantly create a playable testing ground. Press play to test and verify the compilation.

---

## 📦 Assembly Definitions (ASMDEF)
Save System Lite ships with built-in assembly definitions to accelerate compilation and decouple editor-specific code from runtime code:
*   `SaveSystemLite.asmdef` contains the runtime save code.
*   `SaveSystemLite.Editor.asmdef` contains the inspector, Welcome Windows, and demo generator classes.

If your game scripts use a custom assembly definition, make sure to add a reference to `SaveSystemLite` in your `.asmdef` inspector to enable compilation!

> **Warning**: Do not modify files in the `Assets/SaveSystemLite/Editor` folder with custom runtime scripts. Keeping them separated prevents compiler crashes during production standalone game builds.
