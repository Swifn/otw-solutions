# Bandit Level 1 → Level 2

---

## 🎯 Objective

The password for the next level is stored in a file called `-` located in the home directory.

The challenge here is how to handle a **file name that starts with a dash (`-`)**, which normally signifies an option/flag in command-line tools.



---

## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory.

- `cat` - Outputs the content of a file

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
- You should see: 
   ```bash
   -
   ```
5. **Display the contents of `-`**:
```bash
cat ./-
```
-  `./-`  tells the shell to treat `-` as a file in the current directory, not as an option

Thats the password for `bandit2`

---

## 🎉 You’ve now completed Level 1 → Level 2!


---

## 🧠 Lessons Learned / Notes
- Files with names like `-` or those that start with `-` can confuse commands by being mistaken for options.

- Prefixing such filenames with `./` or using `--` is a safe way to reference them.

- Knowing how to escape or work around edge-case filenames is critical in real-world Linux usage and CTFs.
