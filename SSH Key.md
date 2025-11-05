<h1 style="text-align:center;">SSH Key Setup for GitLab on Windows: A Developer’s Guide</h1>

You can generate a new SSH key on your local machine. After you generate the key, you can add the public key to your account on gitlab.com to enable authentication for Git operations over SSH.

### 🛠️ Step 1: Open Git Bash

Git Bash provides a Unix-style terminal on Windows, making it easier to run Git and SSH commands that are native to Linux/macOS environments.

Launch **Git Bash** from your Start menu. 

This gives you a Unix-like terminal on Windows.

### 🔐 Step 2: Generate an SSH Key Pair

SSH keys are a secure way to authenticate with GitLab without typing your password every time. You’ll create a public/private key pair.

Choose your key type:

🔸ED25519 (recommended): Faster, more secure, and modern

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

🔸RSA (fallback for older systems):
```
ssh-keygen -t rsa -b 2048 -C "your_email@example.com"
```

**Flags Explained:**

- `-t`: Specifies the key type.
- `-b`: Bit size (only for RSA).
- `-C`: Adds a comment (usually your email).

This creates a new SSH key and labels it with your email for easy identification.


### 📁 Step 3: Save the Key in Your Desired Path

You can store your SSH key in the default location or choose a custom name to organize multiple keys.

When prompted:

Enter file in which to save the key (/c/Users/user/.ssh/id_ed25519):

**Accept Default Path**

Press Enter to accept the default path:

C:\Users\user\.ssh\id_ed25519

**Or type a custom name:**

Type something like /c/Users/user/.ssh/gitlab_com_ed25519

Git Bash uses /c/Users/... to represent C:\Users\... — don’t be confused by the slashes!

/c/Users/user/.ssh/gitlab_com_ed25519

### 🔒 Step 4: Add a Passphrase (Optional)

A passphrase adds an extra layer of protection to your private key.

You'll see:

Enter passphrase (empty for no passphrase):
Enter same passphrase again:

- A passphrase adds security.
- Leave blank for convenience (less secure)

If you skip the passphrase, Git operations will run without prompting — ideal for frequent use

### ✅ Step 5: Confirm Key Generation

After completing the prompts, you’ll see:

Your identification has been saved in /c/Users/user/.ssh/id_ed25519
Your public key has been saved in /c/Users/user/.ssh/id_ed25519.pub

Key files created

- Private key: `id_ed25519` (keep this secret!)
- Public key: `id_ed25519.pub` (you’ll upload this to GitLab)

Never share your private key. Only the .pub file is meant to be uploaded


### 🧩 Step 6: Add Public Key to GitLab

GitLab needs your public key to recognize and trust your machine.

Copy the public key to clipboard:

```
cat ~/.ssh/id_ed25519.pub | clip
```

This command reads your public key from id_ed25519.pub and copies it to your clipboard

### ➕ Step 7: Add to GitLab:

1. Go to https://gitlab.com and sign in.
2. Click your avatar (top-right) → **Edit profile**.
3. In the left sidebar, go to **SSH Keys**.
4. Paste the key into the **Key** field.
5. Add a **Title** (e.g., “Work Laptop”).
6. Click **Add key**.

GitLab will now recognize your machine for SSH-based Git operations

### 🧭 Step 7: Start SSH Agent and Add Your Key

The SSH agent keeps your key loaded in memory so Git can use it without asking for a passphrase

▶️ Start the agent:

```
eval $(ssh-agent -s)
```

`Agent Pid 12345`

Upon running the command, you’ll receive an output such as Agent pid 12345. This confirms that the SSH agent is now active and prepared to manage your keys

➕ Add your key:

```
ssh-add ~/.ssh/id_ed25519
```

Identity added: /c/Users/sshan/.ssh/id_ed25519 (abc@gmail.com)

If you used a custom name:

```
ssh-add ~/.ssh/gitlab_com_ed25519
```

This step is essential if you added a passphrase or want Git to use your key automatically

### 🗂️ Step 8: Configure SSH for GitLab

Edit your SSH config file:

The SSH config file lets you define which key to use for each host — useful if you manage multiple GitLab accounts or keys

```
nano ~/.ssh/config
```

🔧 Add Configuration

```
# GitLab.com
Host gitlab.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519

# Private GitLab instance
Host gitlab.company.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519
```

If you used a custom filename:

```
IdentityFile ~/.ssh/gitlab_com_ed25519
```

Save and exit

- Press Ctrl+O, Enter to save
- Press Ctrl+X to exit

This ensures Git uses the correct key when connecting to GitLab

### 🧪 Step 9: Test SSH Connection

Run this command to check if the connection is working properly

```
ssh -T git@gitlab.com
```

First time, you'll see:

The authenticity of host 'gitlab.com' can't be established...
Are you sure you want to continue connecting (yes/no)?

Type:
yes

Expected output:

Welcome to GitLab, @Your_Username!

This confirms your SSH setup is working and GitLab recognizes your key.

🚀 Step 10: Clone Your Repository

Use Git Bash to clone via SSH:

git clone git@gitlab.com:Your_Username/my-first-repo.git /c/Users/sshan/OneDrive/Desktop/repo_name

You're now ready to work with GitLab repositories using SSH on Windows!
