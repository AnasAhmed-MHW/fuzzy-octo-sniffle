---
title: Developers Setup
nav_order: 3
last_modified_date: 2025-01-20 12:00
---

# Developers Setup (Mac)

<br> 

{: .important}
You will need some Admin permissions to get most of this installed and configured. We recommend asking IT to share temporary Admin access. 

## Software Installation:

1. **Homebrew:** Install Homebrew package manager.
   <br>Website: [brew.sh](https://brew.sh/)
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

    Make sure to follow the instructions at the end - there is something to ensure it gets added to the `$PATH`

    More specifically, to ensure brew can be run from any new terminal session without manually updating the `$PATH` each time, follow these steps:

    1. Gain access to sudo privilege from admin user (IT people can help with that) and then, open the `/etc/paths` file using `sudo` and `nano` to edit the `$PATH`:
    ```bash
    sudo nano /etc/paths
    ```

    2. Add the following line at the end of the file to include Homebrew's location in the `$PATH`:
    ```bash
    /opt/homebrew/bin
    ```

    3. After adding the line, save the file and exit the editor:

    * Press `Control + O` to save the file.
    * Press `Return` (or `Enter`) to confirm the file name.
    * Press `Control + X` to exit `nano`.

    Now, `brew` should be accessible from any new terminal session. Consequently, all software installed via `brew` will also be accessible.

2. **oh-my-zsh:** Install oh-my-zsh for enhanced terminal experience.
   <br>Website: [ohmyz.sh](https://ohmyz.sh/#install)
    ```bash
    sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```

3. **AWS CLI:** Install AWS Command Line Interface.
   <br>Documentation: [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
   ```bash
   curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
   sudo installer -pkg AWSCLIV2.pkg -target /
   ```

4. **Pyenv:** Python version management tool.
    ```bash
    brew install pyenv
    ```

5. **Poetry:** Python dependency management and packaging tool.
    ```bash
    brew install poetry
    ```

6. **MySQL:** 
    ```bash
    brew install mysql
    ```

7. **Node.js & npm:** JavaScript runtime and package manager. allows you to run `npm`
    ```bash
    brew install node
    ```

8.  **Amplify CLI:** Command-line interface for AWS Amplify.
    ```bash
    npm install -g @aws-amplify/cli
    ```    

9. **Databricks CLI**

    Documentation: [Databricks CLI Installation Guide](https://docs.databricks.com/en/dev-tools/cli/install.html#homebrew-install)
    ```bash
    brew tap databricks/tap
    brew install databricks
    ```

10. **Databricks x GitHub:**
    
    To connect Databricks to the GitHub

    1. **Authenticate via OAuth** 

        Attempt to authenticate using GitHub OAuth with a one-time login from Databricks by following the instructions [here](https://docs.databricks.com/en/repos/get-access-tokens-from-git-provider.html#link-your-github-account-using-databricks-github-app). This method may grant you the necessary permissions to clone repositories directly from GitHub.

    2. **Create a Fine-Grained Personal Access Token** 

        If OAuth does not provide the required permissions to clone the repository, follow these steps: 

        1. Create a fine-grained personal access token by following the instructions [here](https://docs.databricks.com/en/repos/get-access-tokens-from-git-provider.html#connect-to-a-github-repo-using-a-fine-grained-personal-access-token).
        2. When configuring the token, ensure that the following repository permissions are set with `Read and Write` access (additional permissions may be added as needed):
            - Actions
            - Contents
            - Pull Requests
            - Commit Statuses
        3. Request access from the owner of the GitHub team.
        4. Once the token is created, copy it and go to **Databricks Settings -> Linked Accounts**, and remove the OAuth connection to GitHub (if added). Then, add the personal access token you created. After this and once your request is approved, you should be able to clone repositories within Databricks.


<br>

{: .important-title}
> Verify
> - To verify installed packages, run `brew list` in the terminal.
> - Git should already be installed. You can verify by running `git --version`.
> If you get a git not found error:
> ```
> brew install git
> ```

<br>

## Recommended Software for Mac Setup:

1. **Visual Studio Code (VSCode):**
    <br>Website: [Visual Studio Code](https://code.visualstudio.com/)
    ```bash
    brew install --cask visual-studio-code
    ```

1. **PyCharm (Community Edition):**
    - Download the Toolbox and use the Interface to manage apps from there.
    - Website: [JetBrains Toolbox](https://www.jetbrains.com/toolbox-app/)

2. **Docker:**
    <br>Website: [Docker](https://www.docker.com/products/docker-desktop)
    ```bash
    brew install --cask docker
    ```

3. **Sublime Text:**
    <br>Website: [Sublime Text](https://www.sublimetext.com/)
    ```bash
    brew install --cask sublime-text
    ```

4. **iTerm2:**
    <br>Website: [iTerm2](https://iterm2.com/)
    ```bash
    brew install --cask iterm2
    ```

5. **Sequel Ace or Sequel Pro:**
    <br>Sequel Pro Website: [Sequel Pro](https://www.sequelpro.com/)
    ```bash
    brew install --cask sequel-ace
    ```

6. **Bitwarden:**
    <br>Website: [Bitwarden](https://bitwarden.com/)
    ```bash
    brew install --cask bitwarden
    ```

    {: .warning}
    **March 2024** If you want biometric browser integration (ie fingerprint to unlock chrome, firefox) you will need to use bitwarden from the app store.
    Version from brew/ in-website will not allow this browser integration.

7. **Anaconda:**
    <br>Website: [Anaconda](https://www.anaconda.com/products/distribution)
    ```bash
    brew install --cask anaconda
    ```

8.  **Zoom**
    <br>Website: [Zoom](https://zoom.us/download)
    ```bash
    brew install --cask zoom
    ```

9.  **Egnyte Core**
    <br>Website: [Engyte Core](https://helpdesk.egnyte.com/hc/en-us/articles/6688611695373-New-Desktop-App-Core-for-Mac)
    - MediaHub Egnyte Domain is `https://mediahubemea.egnyte.com/`

    {: .warning}
    IPG will be removing Egnyte as a tool in Q1 of 2025 therefore this will become redundant

10. **Rectangle:** 
    ```bash
    brew install --cask rectangle
    ```

11. **Maccy:** 
    ```bash
    brew install --cask maccy
    ```


With iTerm2 / Terminal you are able to make some modifications that make life a little easier. 
Within your `~/.zshrc` file

```
plugins=(
    git
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```

you will need to run

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

