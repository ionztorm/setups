# SSH for github from scratch

<!--toc:start-->
- [SSH for github from scratch](#ssh-for-github-from-scratch)
  - [Create the SSH key](#create-the-ssh-key)
  - [Add the SSH key to the agent](#add-the-ssh-key-to-the-agent)
    - [Start the agent](#start-the-agent)
    - [Create your config file and edit it](#create-your-config-file-and-edit-it)
    - [Add the key to the agent](#add-the-key-to-the-agent)
  - [Add to github](#add-to-github)
    - [Copy the key to your clipboard](#copy-the-key-to-your-clipboard)
    - [Save in github](#save-in-github)
<!--toc:end-->

Note: this setup follows the mac process. For linux, the process is similar, but the commands may differ.For

## Create the SSH key

Open your terminal and enter:

```bash
ssh-keygen -t ed25519 -C <your_email@example.com>
```

You'll be prompted to enter a file name for the key. I like to use the default postfixed with `<host>_<purpose>`, for example:

```bash
/Users/<username>/.ssh/id_ed25519_github_work
/Users/<username>/.ssh/id_ed25519_github_personal
```

You'll then be prompted to enter a passphrase. This is optional, but I recommend using one.


## Add the SSH key to the agent

### Start the agent


```bash
$ eval "$(ssh-agent -s)"
```

### Create your config file and edit it

```bash
mkdir ~/.ssh
touch ~/.ssh/config
```

```bash
Host github-work
  HostName github.com
  User git
  AddKeysToAgent yes
  UseKeychain yes # omit this line if you did not add a passphrase
  IdentityFile ~/.ssh/id_ed25519_github_work
Host github-personal
  HostName github.com
  User git
  AddKeysToAgent yes
  UseKeychain yes # omit this line if you did not add a passphrase
  IdentityFile ~/.ssh/id_ed25519_github_personal
```
### Add the key to the agent

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_github_work
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_github_personal
# --apple-use-keychain is not necessary if you did not add a passphrase
```
## Add to github

### Copy the key to your clipboard

```bash
pbcopy < ~/.ssh/id_ed25519_github_work.pub
pbcopy < ~/.ssh/id_ed25519_github_personal.pub
```

### Save in GitHub

Go to your GitHub account settings and add the key to your SSH keys.


To understand how to use multiple keys with github projects, see [My multi GitHub ssh guide](./multi-github-ssh.md)
