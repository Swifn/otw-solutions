# Bandit Level 19 → Level 20

---

## 🎯 Objective

You are provided with a **setuid binary** in the home directory.

Your goal is to **use this binary to access the password** for the next level, which is stored in the usual place:
`/etc/bandit_pass/bandit20`.

---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory
- `cat` - Outputs the content of a file
- `./<binary>` - Executes a binary file in the current directory


---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
  - You should see:
    ```bash
     bandit20-do
    ```


5. **Run `bandit20-do` without arguments to see the usage**:
```bash
./bandit20-do
```
 - You should see:
    ```bash
    Run a command as another user.
    Example: ./bandit20-do id
    ```

6. **Use it to read the password file owned by `bandit20`**
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```



Thats the passwprd for `bandit19`

---

## 🎉 You’ve now completed Level 19 → Level 20!


---

## 🧠 Lessons Learned / Notes
- `setuid` binaries are often used in privilege escalation - understanding how they work is essential in both systems programming and cybersecurity.

- Running a setuid binary **with arguments** allows you to perform restricted tasks with higher privileges - be cautious with such binaries in real-world systems.
