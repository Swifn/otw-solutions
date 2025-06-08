# Bandit Level 20 → Level 21

---

## 🎯 Objective

Use a setuid binary in the home directory to retrieve the password for `bandit21`.
The binary connects to `localhost:<port>` and:

- Sends the password from `bandit20` as input.

- If the server replies with the correct password, it returns the password for `bandit21`.

---


## 🛠️ Commands Used (with explanations)

- `ls` - Lists files in the current directory

- `nmap` - Scans for open ports

- `nc` - Netcat, used to create TCP connections or listeners

  - `-l` - Starts a listener mode

  - `-p` - Specifies the port number

- `&` - Runs the command in the background


---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
  - You should see:
    ```bash
    suconnect
    ```
    
5. **Check how the binary works**:
```bash
./suconnect
```
  - You should see:
    ```bash
    Usage: ./suconnect <portnumber>
    This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
    ```


6. **Find open ports**:
```bash
nmap localhost
```
  - You should see:
    ```bash
    PORT      STATE SERVICE
    22/tcp    open  ssh
    1111/tcp  open  lmsocialserver
    1840/tcp  open  netopia-vo2
    4321/tcp  open  rwhois
    4444/tcp  open  krb524
    8000/tcp  open  http-alt
    12345/tcp open  netbus
    30000/tcp open  ndmps
    50001/tcp open  unknown
    ```

7. **Test each port using `suconnect`**:
```bash
./suconnect <port>
```
  - You should see (once the correct port is identified)
    ```bash
    Read: <bandit20_password>
    Password matches, sending next password
    ```
      - Although is states "sending next password", there is no password visible - this is correct
      - We have not set a listener to retrieve the response

8. **Set up a `nc` listener to respond with the Bandit 20 password**:
```bash
echo "<bandit20_password>" | nc -l -p <port> &
```
  - You should see
    ```bash
    [<job_number>] <process_id>
    ```
    - This incidates that the process is running in the background

9. **Run the `suconnect` binary to connect to the listener**:
```bash
./suconnect <port>
```
  - You should see
    ```bash
    Read: <bandit20_password>
    Password matches, sending next password
    <bandit21_password>
    [<job_number>]+  Done                    echo "<bandit20_password>" | nc -l -p <port>
    ```
     



Thats the password for `bandit21`

---

## 🎉 You’ve now completed Level 20 → Level 21!


---

## 🧠 Lessons Learned / Notes
- Creating a **local TCP service** that interacts with a privileged binary.

- Understanding **TCP communication** and **process control** (background jobs) is critical for multi-step interactive tools.

- `nc` is incredibly useful for quick server/client testing.
