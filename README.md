# 🔐 Adding SSH Key to GitHub (Windows)

This guide helps you set up SSH authentication for GitHub on Windows.

---

## 🔧 Step 1: Check for Existing SSH Keys

Open **Git Bash** or **PowerShell** and run:

```bash
ls -al ~/.ssh
```

If you see files like `id_rsa` and `id_rsa.pub`, you may already have an SSH key.  
If not, continue to create one.

---

## 🗝️ Step 2: Generate a New SSH Key

Run this command (replace with your email):

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

If your system doesn’t support `ed25519`, use:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

When prompted:

- Press **Enter** to accept the default file location.
- Optionally, set a **passphrase** for extra security.

This creates:

```
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

---

## 🔑 Step 3: Start the SSH Agent and Add Your Key

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

If you used RSA instead, change the filename accordingly.

---

## 📋 Step 4: Copy Your Public Key

Copy your public key to the clipboard:

```bash
clip < ~/.ssh/id_ed25519.pub
```

If that doesn’t work, open and copy it manually:

```bash
cat ~/.ssh/id_ed25519.pub
```

Then copy the full text that starts with `ssh-ed25519`.

---

## 🌐 Step 5: Add the Key to Your GitHub Account

1. Go to [GitHub → Settings → SSH and GPG Keys](https://github.com/settings/keys)  
2. Click **New SSH key**
3. Add a descriptive title (e.g., “Windows Laptop”)
4. Paste your key into the field
5. Click **Add SSH key**

---

## ✅ Step 6: Test the Connection

Run this command to test your SSH connection:

```bash
ssh -T git@github.com
```

You should see:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 🧭 Step 7: Set SSH as the Default Remote (Optional)

If you cloned a repository using HTTPS, you can switch to SSH:

```bash
git remote set-url origin git@github.com:username/repository.git
```

---

**You’re all set! 🎉**  
Your Windows system is now configured to use SSH with GitHub.
