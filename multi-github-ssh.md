# Use multiple SSH keys for multiple GitHub accounts

This assumes you have already created your SSH keys. If you haven't, see [SSH from scratch](./ssh-from-scratch.md).

## Using the correct SSH on GitHub push/fetch for your repo

1. Have multiple ssh keys in ~/.ssh such as:

```bash
id_ed25519_github_personal
id_ed25519_github_work
```

2. Open your ssh config

```bash
nvim ~/.ssh/config
```

3. Create a host for each key

```bash
Host github-personal
  HostName github.com
  User git
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519_github_personal

Host github-work
  HostName github.com
  User git
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519_github_work
```
4. Check they're both added:

```zsh
ssh-add -l
```

add if not:

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_github_work
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_github_personal
# omit --apple-use-keychain if you did not add a passphrase
```
Enter your passphrase when prompted.

4. Navigate to the project directory

5. Set local git config to the appropriate username

```bash
git config user.name "<github username>"
git config user.email "<github email>"
```

6. Check they saved

```bash
git config user.name
git config user.email
```

7. Set the remote origin to the ssh key you want to use

```bash
# for work repo
git remote add origin git@github-work:<username>/<repo>.git

# for personal repo
git remote add origin git@github-personal:<username>/<repo>.git

# to update an existing remote simply replace 'add' above with set-url
```
