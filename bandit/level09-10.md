# Bandit Level 9 → Level 10

---

## 🎯 Objective

The password for the next level is stored in the file `data.txt`.  
It is found among **a few human-readable strings**, and is **preceded by several `=` characters**.



---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory.
- `strings` - Extracts human-readable text from a binary file
- `grep` - Searches for lines that match a pattern




---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
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
  i�|�/2���a8���tT�9�$��(@'°w0�0o����_�xL*���g�ʲR>��wMs�� ��V����uuF�I�-S����A����"|����;&s��d��Df,����a���%�xe-��
  �1`$9k�-gwp
  ...
  ```

6. **Display and filter the contents of the file `data.txt`**:
```bash
strings data.txt | grep ====
```


Thats the password for `bandit9`

---

## 🎉 You’ve now completed Level 8 → Level 9!


---

## 🧠 Lessons Learned / Notes
- `strings` is extremely useful for extracting text from binary or unknown-format files.

- Grepping for known patterns like `===` can help pinpoint useful lines.

- This level introduces basic binary analysis - more of that will come in later challenges.
