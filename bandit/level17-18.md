# Bandit Level 17 → Level 18

---

## 🎯 Objective

You are given two files in the home directory:

- `passwords.old`

- `passwords.new`

The password for the next level is the only line that is different between the two files - i.e., it was changed in `passwords.new`.

---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory

- `cat` - Displays the contents of a file

- `diff` - Compares two files line-by-line and shows differences



---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh -i /tmp/tmp.31SMTd6sGw bandit17@localhost -p 2220
```
- I used a tmp file in `bandit16` to store the RSA private key retrieved from the previous level

3. **List the contents of the home directory**:
```bash
ls
```
  - You should see:
    ```bash
    passwords.old  passwords.new
    ```

4. **Display the contents, use `diff` to find the difference**:
```bash
diff passwords.old passwords.new
```
  - You should see:
    ```bash
    42c42
    < oldpassword
    ---
    > newpassword
    ```


Thats the password for `bandit18`

---

## 🎉 You’ve now completed Level 17 → Level 18!


---

## 🧠 Lessons Learned / Notes
- `diff` is a great tool to compare versions of files, especially for config changes or spotting subtle edits.

- Pay attention to the line prefix in `diff`:

  - `<` means line from the first file

  - `>` means line from the second file (which you want in this level)
