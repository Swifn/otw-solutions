# Bandit Level 2 → Level 3

---

## 🎯 Objective

The password for the next level is stored in a file called `spaces in this filename`, located in the home directory.

The challenge is learning how to work with filenames that contain **spaces** in the shell.

---

## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory.

- `cat` - Outputs the content of a file

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
- You should see: 
   ```bash
   spaces in this filename
   ```
5. **Display the contents of `-`**:
```bash
cat "spaces in this filename"
```
-  Surrounding the filename in quotes allows the shell to interpret it as a single argument.

Thats the password for `bandit3`

---

## 🎉 You’ve now completed Level 2 → Level 3!


---

## 🧠 Lessons Learned / Notes
- Filenames with spaces must be quoted or have the spaces escaped.

- Always use `tab` to autocomplete file names - it can reduce errors and reveal formatting issues.
