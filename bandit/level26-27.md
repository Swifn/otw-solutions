# Bandit Level 26 → Level 27
---

## ⚠️ Disclaimer

This level is a continuation of level 25-26:

https://github.com/Swifn/otw-solutions/blob/main/bandit/level25-26.md

---

## 🎯 Objective

You already broke into the shell for **bandit26** in the previous level. Now:

You're inside a real shell as **bandit26**

Your goal is simple: **read the password for bandit27**


---


## 🛠️ Commands Used (with explanations)

`ls` - Lists files and directories in the current working directory

`cat` - Outputs the contents of a file

---

## 🚀 Steps to Solve

1. **List the contents of the home directory**:
```bash
ls
```
  - You should see:
    ```bash
    bandit27-do  text.txt
    ```

2. **Run `bandit27-do`**:
```bash
./bandit27-do
```
  - You should see:
    ```bash
    Run a command as another user.
    Example: ./bandit27-do id
    ```

3. **Read `bandit27` password**:
```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```
  - You should see:
    ```bash
    <bandit27_password>
    ```



## 🎉 You’ve now completed Level 26 → Level 27!


---

## 🧠 Lessons Learned / Notes
- Once you’ve gained a real shell, everything else becomes simple - standard commands like `cat` and `ls` do the job.

- Don’t overthink levels like this - sometimes the only task is to **recognise that you already have access** and just need to retrieve the flag.

- Always check `/etc/bandit_pass/` for the next password unless the level tells you otherwise.

