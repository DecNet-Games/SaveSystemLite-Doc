---
layout: default
title: Core Features
nav_order: 4
has_children: true
---

# Core Features

Save System Lite provides a robust, professional-tier set of features designed to make local storage in Unity simple, reliable, and extremely fast.

Explore our feature documentation sections below:

---

## 💾 [1. Multi-Slot Management](slots.html)
Save System Lite supports three isolated, slot-based file instances (Slot 0, Slot 1, and Slot 2) natively. Changing slots is done instantly with a single method. The system handles file paths, WebGL keys, and local directories automatically.

---

## 🗄️ [2. Key-Value Database](key-value-db.html)
Save individual keys and values dynamically inside any save slot! Bypasses traditional full JSON file limits. We've built custom serializer wrappers so structures like `Vector3`, `Quaternion`, and `Color` work flawlessly without crashes or third-party DLL dependencies.

---

## 🤖 [3. Lite Auto-Save Component](auto-save.html)
Automate saving without writing code! Drag-and-drop the `SaveSystemLiteAutoSave` script onto any GameObject in your scene to track and restore position and rotation automatically on disable or application shutdown.
