# Bandit Level 5 → Level 6

---

## 🎯 Objective

Find the password for the next level. It's stored in a file **somewhere under the `inhere/` directory**, and that file must meet **all** of the following criteria:

- Human-readable
- Exactly **1033 bytes** in size
- **Not executable**


---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory.

- `cat` - Outputs the content of a file

- `cd` - Change the directory.

- `find` - searches for files matching specific conditions
   - `-type f` - only look for files
   - `-size 1033c` - exactly 1033 bytes (c = bytes).
   - `-not -executable` - file must **not** be executable

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
- You should see: 
   ```bash
   inhere
   ```
5. **Change the directory to `inhere`**:
```bash
cd inhere/
```

6. **List the contents of the `inhere` directory**:
```bash 
ls
```
- You should see:
   ```bash
   maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
   maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
   maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
   ```

7. **Find the file with the given criteria**:
```bash
find ./* -type f -size 1033c -not -executable
```
- You should see:
   ```bash
   ./maybehere07/.file2
   ```

8. **Display the contents of the file**:
```bash
cat ./maybehere07/.file2
```

Thats the password for `bandit6`

---

## 🎉 You’ve now completed Level 5 → Level 6!


---

## 🧠 Lessons Learned / Notes
- `find` is one of the most powerful tools in Linux - you can combine flags to filter files by type, size, permissions, etc.

- Using `-not -executable` ensures you skip binary programs or scripts.

- Always verify your results with `file` before using `cat` - some files can break your terminal view if opened directly.
