# 📂 Organizing Files in Git Using Shell Commands

## 🚀 The Problem: A Messy Project Folder
Imagine you have a project folder filled with different types of files—PDFs, Markdown files, and text files—all scattered everywhere. It’s getting hard to manage, and your Git repository looks cluttered. How do we **organize** these files into dedicated folders **without losing Git history**?

💡 **Solution:** Move similar files into dedicated folders using simple shell commands while ensuring Git properly tracks the changes.

---

## 🔍 Step-by-Step Guide to Organizing Files

### **1️⃣ Moving PDF Files into a `pdf-files/` Directory**
We’ll create a `pdf-files/` directory and move all `.pdf` files inside it.

```bash
# Step 1: Make sure you are in the root directory of your project
cd /path/to/your/project  # Change this to your actual project path

# Step 2: Create a directory for PDF files
mkdir pdf-files

# Step 3: Move all PDFs into the new directory
mv *.pdf pdf-files

# Step 4: Verify the move
ls pdf-files  # Should display all your PDF files

# Step 5: Stage and commit the changes
git add .
git commit -m "Moved all PDF files to pdf-files directory"
```

---

### **2️⃣ Moving Markdown Files (`.md`) into `markdown-files/`**
We’ll do the same for `.md` files.

```bash
# Step 1: Create a directory for Markdown files
mkdir markdown-files

# Step 2: Move all Markdown files
mv *.md markdown-files

# Step 3: Verify the move
ls markdown-files

# Step 4: Stage and commit in Git
git add .
git commit -m "Moved all Markdown files to markdown-files directory"
```

---

### **3️⃣ Moving Text Files (`.txt`) into `code-text-files/`**
For `.txt` files, we’ll move them into `code-text-files/`.

```bash
# Step 1: Create a directory for text files
mkdir code-text-files

# Step 2: Move all text files
mv *.txt code-text-files

# Step 3: Verify the move
ls code-text-files

# Step 4: Stage and commit in Git
git add .
git commit -m "Moved all text files to code-text-files directory"
```

---

## 🤔 **Why We Use `git add .` Instead of `git add -A`?**
When moving files, Git sees them as **deleted from the old location and added to the new location**. To ensure Git tracks the move properly, we use:

✅ `git add .` → Adds all **new and modified** files in the current directory.

🚀 This works fine for us since we are working inside our project’s root directory. If we were making changes across different parts of the repo, we might use `git add -A`.

---

## 🎯 **Final Thoughts**
- **Organization is key** to maintaining a clean and manageable Git repository.
- **Using simple `mv` commands**, we can move files while keeping Git aware of changes.
- **Git is smart enough** to recognize renames, avoiding unnecessary delete/add actions.
- **Always run `git status`** to double-check what’s being tracked before committing.
- **This method works for any file type!** Whether it's `.json`, `.csv`, `.jpg`, `.mp4`, or any other extension, just replace the file type in the command (e.g., `mv *.json json-files`).

🛠️ **With just a few commands, our project goes from a messy folder to a well-structured repo!** 🚀
