# Bandit Level 21 → Level 22

---

## 🎯 Objective

A program is being run **automatically by cron** (a scheduled task runner).
Your goal is to find **what command is being executed**, understand **what it does**, and use that to obtain the password for `bandit22`.


---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files and directories
- `cat` - Displays the contents of a file
  
---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **Look inside `/etc/cron.d/` for cron job**:
```bash
ls /etc/cron.d/
```
  - You should see:
```bash
clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  otw-tmp-dir  sysstat
```

5. **Read the contents of the cron job**:
```bash
cat /etc/cron.d/cronjob_bandit22
```
  - You should see:
    ```bash
    @reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    ```
    
6. **Read the script that is being run**:
```bash
cat /usr/bin/cronjob_bandit22.sh
```
  - You should see:
       ```bash
       #!/bin/bash
       chmod 644 /tmp/<tmp_file>
       cat /etc/bandit_pass/bandit22 > /tmp/<tmp_file>
       ```

7. **Read the contents of that file**:
```bash
cat /tmp/<tmp_file>
```

Thats the password for `bandit22`

---

## 🎉 You’ve now completed Level 21 → Level 22!


---

## 🧠 Lessons Learned / Notes
- `cron` jobs are a common way to automate repetitive tasks.

- Cron files live in `/etc/cron.d/` and follow a specific format (`man 5 crontab` explains it).

- Watching **where scheduled scripts store their output** can give clues about what they’re doing - and what you can exploit or read.
