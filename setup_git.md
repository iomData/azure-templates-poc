**Let’s Supercharge Your Git SSH Setup! 🚀**

Paste this into your OneNote for quick reference.

---

## 1. Prerequisites

* Ensure you have Git installed.
* Open your terminal (macOS/Linux) or Git Bash (Windows).

---

## 2. Check for Existing SSH Keys

```bash
ls ~/.ssh/id_*.pub
```

* If you see `id_rsa.pub` or `id_ed25519.pub`, you already have a key pair.
* Optionally back them up before regenerating.

---

## 3. Generate a New SSH Key

Use the modern Ed25519 algorithm:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

* **File location:** press **Enter** to accept `~/.ssh/id_ed25519`.
* **Passphrase:** highly recommended—type one (you’ll unlock it with your fingerprint or agent).

---

## 4. Start the SSH Agent & Add Your Key

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

> Your agent now holds your unlocked key so you don’t type your passphrase on every Git push.

---

## 5. Copy Your Public Key to Clipboard

* **macOS:**

  ```bash
  pbcopy < ~/.ssh/id_ed25519.pub
  ```
* **Linux (with xclip):**

  ```bash
  xclip -sel clip < ~/.ssh/id_ed25519.pub
  ```
* **Windows (Git Bash):**

  ```bash
  clip < ~/.ssh/id_ed25519.pub
  ```

---

## 6. Add Your SSH Key to GitHub (or Other Host)

1. **GitHub:** Settings → **SSH and GPG keys** → **New SSH key** → paste → **Save**.
2. **GitLab:** User Settings → **SSH Keys** → **Add key** → paste → **Add key**.
3. **Bitbucket:** Personal Settings → **SSH Keys** → **Add key** → paste → **Add key**.

---

## 7. Handle SAML-SSO Enforcement (If Applicable)

Your organization enforces SAML SSO, so you must authorize your SSH key:

1. On GitHub, go to **Settings → SSH and GPG keys**.
2. Click your key (e.g. **id\_ed25519**).
3. Under **“Authorization for SET-Apps”**, click **Authorize**.

---

## 8. Test Your SSH Connection

```bash
ssh -T git@github.com
```

You should see:

> “Hi `username`! You’ve successfully authenticated…”

---

## 9. (Alternative) Clone over HTTPS with a SAML-Authorized PAT

1. Generate a Personal Access Token (repo scope) under **Developer settings → Personal access tokens**, and authorize it for your org.
2. Clone using HTTPS, entering your PAT as the password:

   ```bash
   git clone https://github.com/SET-Apps/vsc-process-testing..git vsc-process-testing
   ```

---

## 10. Initialize & Push a New Repo

```bash
mkdir my-project
cd my-project
git init
git remote add origin git@github.com:username/my-project.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

No passwords—just pure SSH key magic! 🗝️
