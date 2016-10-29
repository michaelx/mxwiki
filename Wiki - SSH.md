# Connect

```sh
ssh username@host.xy
```

With custom port:

```sh
ssh -p 22022 username@host.xy
```

# Disconnect

`ctrl + d`

# Create key

First, check for existing keys:

```sh
ls -al ~/.ssh
```

Create a new key if necessary:

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Ensure ssh-agent is enabled:

```sh
eval "$(ssh-agent -s)"
```

Add key to ssh-agent:

```sh
ssh-add ~/.ssh/id_rsa
```

# Copy public key to server

```sh
ssh-copy-id -i ~/.ssh/id_rsa.pub username@host.xy
```

If `ssh-copy-id` is not yet installed: `brew install ssh-copy-id`