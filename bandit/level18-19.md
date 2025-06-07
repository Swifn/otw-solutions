# Bandit Level 18 → Level 19

---

## 🎯 Objective

The password for the next level is stored in a file called `readme` in the home directory. However, the `.bashrc` file has been modified to automatically log you out upon login, making it difficult to interact normally with the shell.

---


## 🛠️ Commands Used (with explanations)

- `cat` - Outputs the content of a file

- `ls` - Lists files in the current directory

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Connect using SSH with a command executed immediately**:

```bash
 ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

3. **Enter the password**

Thats the password for `bandit19`

---

## 🎉 You’ve now completed Level 18 → Level 19!


---

## 🧠 Lessons Learned / Notes
- `.bashrc` can contain commands that execute on shell startup - and can be used to prevent normal login.

- Passing commands directly to SSH lets you work around startup scripts.

- ssh `user@host <command>` is a powerful way to run remote commands non-interactively.
