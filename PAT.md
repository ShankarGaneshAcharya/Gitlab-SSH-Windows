# Create and Configure a GitLab Personal Access Token in VS Code

## 🧭 Step 1: Install the GitLab Workflow Extension

1. Open **Visual Studio Code**.
   
2. Go to the **Extensions** panel (`Ctrl+Shift+X` or `Cmd+Shift+X` on macOS).
   
3. Search for **GitLab Workflow**.
   
4. Click **Install**.

> [!Note] 
> This extension integrates GitLab features like issues, merge requests, and pipelines directly into VS Code.


## 🛠️ Step 2: Create a Personal Access Token (PAT) on GitLab

1. Log in to your GitLab account: https://gitlab.com
(or your self-hosted GitLab instance, e.g., `https://gitlab.company.com`).

2. Click your avatar (top-right) → **Edit profile** → **Access Tokens** (or **Personal Access Tokens** in newer versions)..

3. Fill out the form:
    * **Name:** e.g., VSCode Integration
    * **Expiration date:** Optional, but **recommended**
    * **Scopes:** Select:
      * `read_user`
      * `api`
      * `read_repository`
      * `write_repository`

4. Click Create personal access token.

5. Copy the token immediately — GitLab will not show it again.

> [!Note]
> Store this token securely (e.g., in a password manager).