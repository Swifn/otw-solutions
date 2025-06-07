# Bandit Level 14 → Level 15

---

## 🎯 Objective

The password for the next level is stored on the local machine and can be retrieved by **submitting the current level's password to port `30001` on `localhost` using SSL/TLS encryption.**

---


## 🛠️ Commands Used (with explanations)

- `openssl` - Toolkit for SSL/TLS encryption
  - `s_client` - Connects to a remote host using SSL
  - `-connect` - Specifies the host and port to connect to
  - `-ign_eof` - Ignores EOF (End Of File) on the standard input


---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **Use `openssl s_client` to connect to port 30001 and send the password**:
```bash
openssl s_client -connect localhost:30001 -ign_eof
```
- Without -ign_eof, the connection might close too early, causing missed or incomplete output.
- With -ign_eof, OpenSSL keeps the connection open long enough to see the response.

Thats the password for `bandit16`

---

## 🎉 You’ve now completed Level 15 → Level 16!


---

## 🧠 Lessons Learned / Notes
- `openssl s_client` lets you interact with SSL/TLS services manually - useful for debugging or testing encrypted connections.

- If you see responses like `RENEGOTIATING`, it's typically due to not sending input quickly enough

- Secure ports like `30001` are common for encrypted services in real - world applications.
