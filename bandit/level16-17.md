# Bandit Level 16 → Level 17

---

## 🎯 Objective

The password for the next level can be retrieved by **submitting the password of the current level to one port on localhost between `31000` and `32000`**.

---


## 🛠️ Commands Used (with explanations)

- `nmap` - Scans a range of ports to find which are open
  - `-p` - Specifies the port range
  - `localhost` - Scan the current machine
  - `-sV` - Service version detection
  - `-v` - Verbose output
- `openssl s_client` - Connect to a service using SSL/TLS
  - `-connect` - Specifies the host and port
  - `-ign_eof` - Keeps the connection open long enough to read the full response

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **Scan for open ports between `31000` and `32000`**:
```bash
nmap -sV -v localhost -p 31000-32000
```
  - You should see:
    ```bash
    PORT      STATE SERVICE     VERSION
    31046/tcp open  echo
    31518/tcp open  ssl/echo
    31691/tcp open  echo
    31790/tcp open  ssl/unknown
    31960/tcp open  echo
    ```


5. **Connect to the port with the `ssl/unknown` service**:
```bash
openssl s_client -connect localhost:31790 -ign_eof
```
 - The ports with an echo service will just return anything you input back to you

6. **Enter the password**



Thats the RSA private key for `bandit17`

---

## 🎉 You’ve now completed Level 16 → Level 17!


---

## 🧠 Lessons Learned / Notes
- `nmap` is a quick and effective way to scan a port range for active services.

- Knowing how to distinguish between SSL/TLS and plain-text protocols is crucial in network-based challenges.

- Using `openssl s_client` helps you safely interact with encrypted services-critical for secure communication testing.
