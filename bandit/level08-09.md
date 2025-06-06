# Bandit Level 7 → Level 8

---

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, and is **located next to the word "millionth"**.



---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory.
- `sort` - Sorts the file so that duplicate lines are grouped together
- `uniq` - Removes **adjacent** duplicate lines and **prints the first occurrence** of each unique line
  -  `-u` - Shows only unique lines



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
  L3ZCH71RRxt8Kmy3X3R0NqQTmebcmkQ4
  NknAyxnPgpoEcWHizP4TA8ALeIyco1VT
  Fmt5ODm3V6Qf1oTF3qEJNWlVcHFdpbuz
  nOu0uI9qll3ws9FtaQt7mE4ngAmMAsfE
  ...
  ```

6. **Display and filter the contents of the file `data.txt`**:
```bash
sort data.txt | uniq -u
```

Thats the password for `bandit8`

---

## 🎉 You’ve now completed Level 7 → Level 8!


---

## 🧠 Lessons Learned / Notes
- `uniq` works best when input is sorted - otherwise, it only checks adjacent lines.

- `-u` shows only lines that are not duplicated.

- Combining `sort` and `uniq` is a powerful technique for analysing repeated data in files.
