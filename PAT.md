# 🔐 Configure GitLab Personal Access Token in Visual Studio Code

This guide explains how to integrate GitLab with VS Code using the **GitLab Workflow** extension and a **Personal Access Token (PAT)** for authentication.

---

## 🧭 Step 1: Install the GitLab Workflow Extension

1. Open **Visual Studio Code**.
2. Go to the **Extensions** panel:
   - Windows/Linux: `Ctrl+Shift+X`
   - macOS: `Cmd+Shift+X`
3. Search for **GitLab Workflow**.
4. Click **Install**.

> 💡 The GitLab Workflow extension integrates GitLab features like issues, merge requests, and pipelines directly into VS Code.

---

## 🛠️ Step 2: Create a Personal Access Token (PAT) on GitLab

1. Log in to your GitLab account:
   - [https://gitlab.com](https://gitlab.com), or  
   - your self-hosted instance, e.g., `https://gitlab.company.com`
2. Click your **avatar (top-right)** → **Edit profile** → **Access Tokens**  
   _(or **Personal Access Tokens** in newer GitLab versions)._
3. Fill out the form:
   - **Name:** e.g., `VSCode Integration`
   - **Expiration date:** Optional, but **recommended**
   - **Scopes:** Select at least:
     - `read_user`
     - `api`
     - `read_repository`
     - `write_repository`
4. Click **Create personal access token**.
5. **Copy the token immediately** — you won’t be able to view it again.

> ⚠️ Store this token securely (for example, in a password manager).

---

## 🔑 Step 3: Authenticate the GitLab Extension in VS Code

1. Open the **Command Palette**:
   - Windows/Linux: `Ctrl+Shift+P`
   - macOS: `Cmd+Shift+P`
2. Type and select **GitLab: Authenticate**, then press **Enter**.
3. Choose your GitLab instance:
   - For gitlab.com, Select **GitLab.com**, or  
   - For **self-hosted instances**, enter your full URL (e.g., `https://gitlab.company.com`)
4. Paste your **Personal Access Token** when prompted.
5. Press **Enter** to confirm.

> 🔒 Your token is stored securely using VS Code’s built-in secret storage.

---

## 🧪 Step 4: Verify the Connection

1. Open the **Command Palette** again.
2. Run one of the following commands:
   - `GitLab: Show Issues`
   - `GitLab: Show Merge Requests`
3. If your GitLab issues or merge requests load successfully, the setup worked!

> ✅ You can also check the **Status Bar** — it should show your current GitLab project context.

---

## 🧩 Step 5: Optional – Configure GitLab Extension Settings

1. Go to **File → Preferences → Settings** (or `Ctrl+,`).
2. Search for **GitLab**.
3. Customize options such as:
   - Default GitLab project
   - Issue and merge request templates
   - Pipeline polling intervals
   - Code snippet creation settings

---

