# Bandit Level 22 → Level 23

---

## 🎯 Objective

A script is being run automatically via `cron`. Your goal is to:

- Investigate the cron job

- Understand the script it runs

- Use that knowledge to retrieve the password for `bandit23`



---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files and directories
- `cat` - Displays the contents of a file
  
---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
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
cat /etc/cron.d/cronjob_bandit23
```
  - You should see:
    ```bash
    @reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
    * * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
    ```
    
6. **Read the script that is being run**:
```bash
cat /usr/bin/cronjob_bandit23.sh
```
  - You should see:
       ```bash
       #!/bin/bash
       myname=$(whoami)

       mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

       echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

       cat /etc/bandit_pass/$myname > /tmp/$mytarget
       ```
7. **Simulate what the script does to get the filename**:
```bash
#!/bin/bash
myname=$(whoami)

mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
  - This can be execute in the command line
  - You should see:
    ```bash
    Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/<tmp_file>
    ```
      - Notice how the password file copied is based off of the current user (bandit22)
    
7. **Change the value of `myname` to `bandit23`**:
```bash
#!/bin/bash
myname=bandit23

mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
  - You should see:
    ```bash
    Copying passwordfile /etc/bandit_pass/bandit23 to /tmp/<tmp_file>
    -bash: /tmp/<tmp_file>: Permission denied
    ```

8. **Read the file that contains the password**:
```bash
cat /tmp/<tmp_file>
 ```

Thats the password for `bandit23`

---

## 🎉 You’ve now completed Level 22 → Level 23!


---

## 🧠 Lessons Learned / Notes
- Analysing scripts written by others is a valuable real-world skill.

- `cron` jobs often leave outputs in `/tmp` - watch for these.

- You can simulate parts of a script to understand what files or operations it performs.
