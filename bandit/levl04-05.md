# Bandit Level 4 → Level 5

---

## 🎯 Objective

The password for the next level is stored in the **only human-readable file** in the `inhere` directory.


---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory.

- `cat` - Outputs the content of a file

- `cd` - Change the directory.

- `file` - identifies the type of each file

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
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
     -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
     ```

7. **Display the type of each file**:
```bash
file ./*
```
- `*` Can be used to display all files at once
- You should see:
   ```bash
   ./-file00: PGP Secret Sub-key -
   ./-file01: data
   ./-file02: datA
   ./-file03: data
   ./-file04: data
   ./-file05: data
   ./-file06: data
   ./-file07: ASCII text
   ./-file08: data
   ./-file09: data
   ```

8. **Display the contents of the **ASCII** (human-readable) file**:
```bash
cat ./-file07
```

Thats the password for `bandit5`

---

## 🎉 You’ve now completed Level 4 → Level 5!


---

## 🧠 Lessons Learned / Notes
- The `file` command is extremely useful for quickly identifying what kind of content a file contains.

- Avoid trying to open binary files with `cat` - it can break your terminal view. Use `reset` to recover if needed.

- Filtering for file types is a powerful technique in CTFs and systems work
