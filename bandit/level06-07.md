# Bandit Level 6 → Level 7

---

## 🎯 Objective

Find the password for the next level. It’s stored **somewhere on the server**, and the file must meet **all** of the following criteria:

- Owned by user: `bandit7`
- Owned by group: `bandit6`
- Exactly **33 bytes** in size


---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory.

- `cat`- Outputs the content of a file

- `find` - searches for files matching specific conditions
   - `-type f` - only look for files
   - `-size 33c` - exactly 33 bytes (`c` = bytes).
   - `-group` - only look for file with group
   - `-users` - only look for files owned by
   - `2>/dev/null` - suppress permission denied errors

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
  - You will see:
    ```bash
    ```
    - The file is not in the home directory - it's somewhere on the system

5. **Find the file with the given criteria**:
```bash
 find / -type f -group bandit6 -user bandit7 2>/dev/null
```
- You should see:
   ```bash
   /var/lib/dpkg/info/bandit7.password
   ```

6. **Display the contents of the file**:
```bash
cat /var/lib/dpkg/info/bandit7.password
```

Thats the password for `bandit7`

---

## 🎉 You’ve now completed Level 6 → Level 7!


---

## 🧠 Lessons Learned / Notes
- This is your first time searching outside your home directory - you’re now scanning the whole system.

- Using `2>/dev/null` avoids clutter from permission-denied errors.

- `find` can combine multiple powerful filters - user, group, size, name, and more.
