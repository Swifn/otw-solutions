# Bandit Level 3 → Level 4

---

## 🎯 Objective

The password for the next level is stored in a **hidden file** located inside the `inhere` directory.

---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory.
   - The `-a` flag shows all files, including hidden files (those starting with a dot `.`).

- `cat` - Outputs the content of a file

- `cd` - Change the directory.

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
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
ls -a
```
   - You should see:
   ```bash
   .  ..  ...Hiding-From-You
   ```

7. **Display the contents of the hidden file `...Hiding-From-You`**:
```bash
cat ...Hiding-From-You
```

Thats the password for `bandit4`

---

## 🎉 You’ve now completed Level 3 → Level 4!


---

## 🧠 Lessons Learned / Notes
- Hidden files in Unix-like systems start with a dot (`.`) and are not shown with a plain `ls`.

- Use `ls -a` to see them.

- This level introduces the importance of file visibility and hidden content - a key concept in system security.
