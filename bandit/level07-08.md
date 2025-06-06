# Bandit Level 6 → Level 7

---

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, and is **located next to the word "millionth"**.



---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory
- `cat` - Outputs the content of a file
- `grep` - Searches for lines that match a pattern
  



---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
   - You will see:
     ```bash
     data.txt
     ```


5. **Display the contents of the file `data.txt`**:
```bash
cat data.txt
```
- You should see:
   ```bash
    arborvitaes     cNdqYLXSXwMpdKosUF514S0uABeZZsuw
    toddlers        bkPZfAOV36kRIBlR9SbnmsHtF2ycoaYR
    whimper buefvyS7DVLAPL5ZwyCWYgkCqih3pMCU
    Austronesian    6rAy7x9GodGAFxplk7Zep0m83qwNmDsu
    ...
    ```

6. **Display and filter the contents of the file `data.txt`**:
```bash
grep millionth data.txt
```

Thats the password for `bandit7`

---

## 🎉 You’ve now completed Level 6 → Level 7!


---

## 🧠 Lessons Learned / Notes
- `grep` is perfect for keyword searches inside files - it’s fast and powerful.

- For pattern matching or extracting values next to certain keywords, `grep` is often your first and best tool.

- Always read level descriptions carefully - a single word like "millionth" can be your exact search target.
