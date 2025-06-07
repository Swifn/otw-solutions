# Bandit Level 0 → Level 1

---

## 🎯 Objective

The password for the next level is stored in a file called `readme` located in the home directory. Use this password to log into `bandit1` using SSH. Whenever you find a password for a level, use SSH (on port `2220`) to log into that level and continue the game.

---

## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory.

- `cat` - Outputs the content of a file

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **Once sucessful, list the contents of the home directory**:
```bash
ls
```
- You should see: 
   ```bash
   readme
   ```
5. **Display the contents of `readme`**:
```bash
cat readme
```

Thats the password for `bandit1`

6. **Logout**:
```bash
exit
```
---

## 🎉 You’ve now completed Level 0 → Level 1!


---

## 🧠 Lessons Learned / Notes
- `ls` and `cat` are essential commands for exploring and viewing file contents.


- Always check the current directory for clues or files.

- Save the password somewhere secure - it won't be stored for you.

- Taking notes on each step helps in case you need to return later or explain your solution to someone else.
