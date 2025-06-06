# Bandit Level 11 → Level 12

---

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, where all lowercase and uppercase letters have been **rotated by 13 positions** - a cipher known as **ROT13**.




---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory.
- `cat` - Outputs the content of a file
- `tr` - Translates or deletes characters from input

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
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
  Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
  ```
  - tr 'A-Za-z' 'N-ZA-Mn-za-m' → Applies ROT13 transformation:
      - Each letter is shifted by 13 places.
      - For example: A → N, N → A, a → n, n → a

6. **Display and filter the contents of the file `data.txt`**:
```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

Thats the password for `bandit12`

---

## 🎉 You’ve now completed Level 11 → Level 12!


---

## 🧠 Lessons Learned / Notes
- ROT13 is a simple Caesar cipher used for light obfuscation - it's symmetric, so encoding and decoding use the same operation.

- The `tr` command is a quick and easy way to perform character substitutions or mappings.

- ROT13 isn’t secure for real encryption, but it’s common in puzzles and CTFs.
