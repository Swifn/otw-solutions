# Bandit Level 10 → Level 11

---

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, and it is **encoded in base64**.

You’ll need to decode the contents to find the actual password.


---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory.
- `base64` - Used to encode or decode data in Base64 format
  - `-d` - Converts a Base64-encoded string back into its original form




---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
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
  VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
  ```

6. **Display and decode the contents of the file `data.txt`**:
```bash
base64 -d data.txt
```

Thats the password for `bandit11`

---

## 🎉 You’ve now completed Level 10 → Level 11!


---

## 🧠 Lessons Learned / Notes
- `base64` encoding is often used to encode binary data into readable text.

- `base64 -d`  decodes it back to its original form.

- This is a common technique in web dev, malware analysis, and CTFs.
