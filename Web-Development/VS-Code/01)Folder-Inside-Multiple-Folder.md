# I am inside a folder with multiple folders in it. How do I search for text in a specific folder in the folder?

In **VS Code**, you can search **inside a specific folder only** (not the entire project) very easily.

---

## ✅ Method 1: Search panel + “files to include” (Best way)

1. Open **Search**
   **Mac:** `Cmd + Shift + F`
   **Windows/Linux:** `Ctrl + Shift + F`

2. Type the **text** you want to search

3. In **“files to include”**, specify the folder:

   ```
   src/components/**
   ```

   or

   ```
   backend/**
   ```

4. Press **Enter**

👉 VS Code will search **only inside that folder**

---

## ✅ Method 2: Right-click the folder (Fastest)

1. In the **Explorer sidebar**
2. **Right-click** the folder you want
3. Click **“Find in Folder”**
4. Enter your search text

👉 Searches **only that folder**

---

## ✅ Method 3: Exclude everything else

Use **files to exclude**:

```
!src/components/**
```

Useful when your search is very broad.

---

## 🔍 Folder pattern examples

| Goal                | Pattern                          |
| ------------------- | -------------------------------- |
| All files in folder | `folder/**`                      |
| Only JS files       | `folder/**/*.js`                 |
| React files         | `folder/**/*.{js,jsx}`           |
| Ignore test files   | `folder/**,!folder/**/*.test.js` |

---
