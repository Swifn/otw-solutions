# Bandit Level 15 → Level 15

---

## 🎯 Objective

The password for the next level is stored on the local machine and can be retrieved by submitting the password of the current level to port `30000` on `localhost`.

---


## 🛠️ Commands Used (with explanations)

- `nc` - Netcat, a tool used to read/write data across network connections

  - `localhost` - Refers to the current machine

  - `30000` - The port number Netcat should connect to

---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

5. **Connect port `30000` using Netcat, and enter the password**:
```bash
nc localhost 30000
```
- Your command line might appear blank, but entering the password outputs the flag



Thats the password for `bandit15`

---

## 🎉 You’ve now completed Level 14 → Level 15!


---

## 🧠 Lessons Learned / Notes
- Netcat (`nc`) is a powerful utility that can interact with network services directly.

- Ports like `30000` can host custom services waiting for specific input - common in Capture the Flag (CTF) challenges.

- `localhost` always refers to the system you’re connected to - it doesn’t need an internet connection.
