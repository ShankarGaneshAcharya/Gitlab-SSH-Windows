<h1 style="text-align:center;">SSH Key Setup for GitLab on Windows: A Developer’s Guide</h1>

You can generate a new SSH key on your local machine. After you generate the key, you can add the public key to your account on gitlab.com to enable authentication for Git operations over SSH.

🛠️ Step 1: Open Git Bash
Launch Git Bash from your Start menu. This gives you a Unix-like terminal on Windows.

🔐 Step 2: Generate an SSH Key Pair
Choose your key type:
🔸 For ED25519 (recommended):
ssh-keygen -t ed25519 -C "your_email@example.com"


🔸 For RSA (2048-bit):
ssh-keygen -t rsa -b 2048 -C "your_email@example.com"


- -t: Specifies the key type.
- -b: Bit size (only for RSA).
- -C: Adds a comment (usually your email).

This creates a new SSH key, using the provided email as a label.



📁 Step 3: Save the Key in Your Desired Path
When prompted:
Enter file in which to save the key (/c/Users/user/.ssh/id_ed25519):


Press Enter to accept the default path:
C:\Users\user\.ssh\id_ed25519


Or type a custom name:
/c/Users/user/.ssh/gitlab_com_ed25519


Note: Git Bash uses /c/Users/... to refer to C:\Users\...


🔒 Step 4: Add a Passphrase (Optional)
You'll see:
Enter passphrase (empty for no passphrase):
Enter same passphrase again:


- A passphrase adds security.
- Leave blank if you want passwordless access (less secure but convenient).

✅ Step 5: Confirm Key Generation
You’ll see something like:
Your identification has been saved in /c/Users/user/.ssh/id_ed25519
Your public key has been saved in /c/Users/user/.ssh/id_ed25519.pub


- Private key: id_ed25519 (keep this secret!)
- Public key: id_ed25519.pub (you’ll upload this to GitLab)

🧩 Step 6: Add Public Key to GitLab
Copy the public key to clipboard:
cat ~/.ssh/id_ed25519.pub | clip
# Copies the contents of the id_ed25519.pub file to your clipboard


➕Add to GitLab:
- Go to https://gitlab.com and sign in.
- Click your avatar (top-right) → Edit profile.
- In the left sidebar, go to SSH Keys.
- Paste the key into the Key field.
- Add a Title (e.g., “Work Laptop”).
- Click Add key.

🧭 Step 7: Start SSH Agent and Add Your Key
Start the agent:
eval $(ssh-agent -s)

Agent Pid 12345

Add your key:
ssh-add ~/.ssh/id_ed25519

Identity added: /c/Users/sshan/.ssh/id_ed25519 (shankarganeshacharya@gmail.com)



If you used a custom name:
ssh-add ~/.ssh/gitlab_com_ed25519



🗂️ Step 8: Configure SSH for GitLab
Edit your SSH config file:
nano ~/.ssh/config


Add:
# GitLab.com
Host gitlab.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519

# Private GitLab instance
Host gitlab.company.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519


If you used a custom filename:
IdentityFile ~/.ssh/gitlab_com_ed25519


Save and exit (Ctrl+O, Enter, then Ctrl+X).

🧪 Step 9: Test SSH Connection
Run:
ssh -T git@gitlab.com


First time, you'll see:
The authenticity of host 'gitlab.com' can't be established...
Are you sure you want to continue connecting (yes/no)?

The authenticity of host 'gitlab.com (3765:5849:80:0:g24e:ffsc:9bde:b8b8)' can't be established.
ED25519 key fingerprint is: SHA256:eUXGGm1YGsMAS7vkcx6JOJdOGHPem5gQp4taiCfCLB8
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? Yes

Type:
yes


Then, if everything is set up:
Welcome to GitLab, @shankarganeshacharya!



🚀 Step 10: Clone Your Repository
Use Git Bash to clone:
git clone git@gitlab.com:shankarganeshacharya/my-first-repo.git /c/Users/sshan/OneDrive/Desktop/my-first-repo --progress --recursive



🧠 Final Tips
- Private key: Never share it.
- Public key: Can be reused across GitLab, GitHub, etc. if needed.
- Multiple keys: You can create separate keys for GitHub and GitLab and configure them in ~/.ssh/config.
Would you like help setting up a second key for GitHub or automating this with a script?