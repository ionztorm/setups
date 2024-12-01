## Using the correct SSH on github push/fetch for your repo

1. Have multiple ssh keys in ~/.ssh such as:

```
id_ed25519_github_personal
id_ed25519_github_work
```

2. Open your ssh config

```zsh
nvim ~/.ssh/config
```

3. Create a host for each key

```
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

4. Navigate to the project directory
5. Set local git config

```zsh
git config user.name "<github username>"
git config user.email "<github email>"
```

6. Check they saved

```zsh
git config user.name
git config user.email
```

7. Set the remote origin to the ssh key you want to use

```zsh
# for work repo
git remote add origin git@github-work:<username>/<repo>.git

# for personal repo
git remote add origin git@github-personal:<username>/<repo>.git

# to update an existing remote simply replace 'add' above with set-url
```
