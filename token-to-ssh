Switching from GitHub Token to SSH

I was using a personal access token to push code to GitHub, but I had to enter it every time. To make things easier, I switched to SSH authentication.

Why I switched to SSH

- Personal access tokens expire or need to be entered repeatedly
- SSH works with one-time setup and no repeated authentication
- It is more secure and recommended by GitHub for regular use

Steps followed:

1. Generated an SSH key:

ssh-keygen -t ed25519 -C "yallashellesty@gmail.com"

2. Copied the public key:

cat ~/.ssh/id_ed25519.pub

3. Added the public key to GitHub:
- GitHub > Settings > SSH and GPG keys > New SSH key
- Pasted the key content

Now I can push to GitHub without using a token every time.
