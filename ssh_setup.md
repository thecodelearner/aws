## Checking for existing SSH keys

```sh
$ ls -la ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

*Skip creating new keys if a key [id_rsa.pub | id_ecdsa.pub | id_ed25519.pub] is already present*


## Generating a new SSH key and adding it to the ssh-agent


```sh
$ ssh-keygen -t ed25519 -C "your_email@example.com"
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_ed25519
```

## Adding a new SSH key to your GitHub account & Verifying it

```sh
$ cat ~/.ssh/id_ed25519.pub

# Copy the output to the clipboard and add it to your github account 

$ ssh -T git@github.com

> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
> Are you sure you want to continue connecting (yes/no)? yes


> Hi username! You've successfully authenticated, but GitHub does not
> provide shell access.
```
