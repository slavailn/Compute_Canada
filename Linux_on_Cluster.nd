# Introduction to Using Linux on Compute Canada Clusters

## 🧰 1. Why Linux for HPC
- Compute Canada’s clusters run Linux (e.g., CentOS/Red Hat).
- You interact via **SSH and terminal**, without a graphical interface.
- Windows executables don’t run natively—you’ll be using command-line tools.

---

## 📖 2. Getting Help
- Use **manual pages** to read full documentation:
  ```bash
  man command
  ```
  Exit with `q`.

- Many commands also have built-in help:
  ```bash
  ls --help
  ```

---

## 🔍 3. Navigating the File System
- After SSH login, you land in your `$HOME` directory.
- Avoid filenames with spaces, accents, or special characters.

### Common file and directory commands:

| Task              | Command                        |
|-------------------|--------------------------------|
| List contents     | `ls`, `ls -a`, `ls -l`, `ls -alth` |
| Change directory  | `cd /path/to/dir`              |
| Make directory    | `mkdir my_folder`              |
| Delete file       | `rm filename`                  |
| Remove directory  | `rmdir dirname` or `rm -r dirname` |
| Copy files        | `cp source dest`               |
| Move or rename    | `mv oldname newname`           |

---

## 🔐 4. File Permissions
- Linux files have **owner/group/other** with **rwx** (read/write/execute) permissions.
- View permissions with `ls -l`.
- Modify permissions using `chmod`, change owners with `chown`.

---

## 🧠 5. Viewing and Editing Files

- View files:
  ```bash
  less filename
  ```
  Scroll with arrow keys, exit with `q`.

- Compare files:
  ```bash
  diff file1 file2
  ```

- Search within files:
  ```bash
  grep 'pattern' filename
  ```

---

## ✅ 6. Quick Tips for Compute Canada
- Your `$HOME` directory starts clean; use it for configs, not large data.
- Use `man`, `--help`, and online examples to learn commands.
- Stick to **safe naming** conventions: lowercase, no spaces, no special chars.
- Learn navigation and file ops to work efficiently on the cluster.

---

## 🛠️ Example Workflow

1. **Log in** via SSH into a cluster head node.
2. **Navigate** to your project folder:
   ```bash
   cd ~/projects/your_username/my_project
   ```
3. **Manage data**:
   ```bash
   ls -l            # view files
   mkdir analysis   # create folder
   cp data/*.fastq analysis/
   ```
4. **Inspect files**:
   ```bash
   less analysis/sample1.fastq
   grep '@' analysis/sample1.fastq
   ```
5. **Submit an analysis job**, edit scripts, etc.

---

## 💡 Getting Started
- Consider taking the self-paced SHARCNET “Introduction to the Shell” course.
- Explore basic tutorials on GitHub or the Compute Canada documentation for practical workflows.
