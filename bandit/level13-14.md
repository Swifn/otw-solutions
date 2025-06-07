# Bandit Level 13 → Level 14

---

## 🎯 Objective

The password for the next level is stored in `/etc/bandit_pass/bandit14` but can **only be read by user `bandit14`**.

You are not given the password directly, but instead provided with a **private SSH key** (located in `sshkey.private`) that can be used to log in as `bandit14`.

---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory
- `cat` - Outputs the content of a file
- `ssh` - Secure Shell login command
  - `-i` - Use a specific private key instead of the default one
  - `-p` - Specifies the port number for the SSH connection
  - `user@localhost`
    - `user` - The username you want to log in as
    - `localhost` - The host you’re connecting to

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
  - You will see:
    ```bash
    sshkey.private
    ```


5. **SSH into bandit14 `data.txt`**:
```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

6. **Display the contents of the file `/etc/bandit_pass/bandit14`**:
```bash
cat /etc/bandit_pass/bandit14
```


Thats the password for `bandit14`

---

## 🎉 You’ve now completed Level 13 → Level 14!


---

## 🧠 Lessons Learned / Notes
- SSH keys provide a secure, password-less way to authenticate users.

- `localhost` refers to the same machine you're currently connected to - useful for chaining access when permissions are restricted.
