# Bandit Level 0

## 🎯 Objective

The goal of this level is for you to log into the game using SSH.

- **Host**: `bandit.labs.overthewire.org`
- **Port**: `2220`
- **Username**: `bandit0`
- **Password**: `bandit0`

Once logged in, go to the Level 1 page to continue the game.

---

## 🛠️ Commands Used (with explanations)

- `ssh` — Secure Shell, used to log into the remote system

---

## 🚀 Steps to Solve

1. Open your terminal.
2. Run the following command to log into the server:

   ```bash
   ssh bandit0@bandit.labs.overthewire.org -p 2220
   ```
3. When prompted for a password, enter
   ```bash
   bandit0
   ```
4. If successful, you’ll be logged into the Bandit Level 0 shell.

---

## 🎉 You’ve now completed Level 0!

---

## 📝 Notes
- This level has no puzzle — it’s just practice for SSH login.

- Use the default password bandit0 to get started.

