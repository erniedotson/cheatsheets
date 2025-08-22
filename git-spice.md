# Git Spice Cheatsheet

## Terms

* **CR** - Change Request. Generic term for GitHub Pull Request (PR) or Gitlab Merge Request (MR).
* **submit** - Push changes to git remote.
* **publish** - Create/Update CR.

## CLI Commands

| Description | CLI Command |
| ----------- | ----------- |
| Track an existing branch | `gs branch track` |
| Create a new branch and track it | `gs branch create new-branch-name` |
| Navigate up stack | `gs up` |
| Navigate down stack | `gs down` |
| Restack all branches in current stack | `gs stack restack` |
| Restack current branch and above | `gs upstack restack` |
| Login | `gs auth login` |
| Push branch | `gs branch submit --[no-]publish` |
| Push stack | `gs stack submit --[no-]publish` |
| Config: Use private Github server | `git config --local spice.forge.github.url "https://github.example.com"` |
| Config: Use private Gitlab server | `git config --local spice.forge.gitlab.url "https://gitlab.example.com"` |
| Config: Change default submit behavior to NOT publish (create a CR) | `git config --local spice.submit.publish "false"` |

## Setting up a Gitlab Personal Access Token

1. Go to [https://gitlab.com/-/user_settings/personal_access_tokens](https://gitlab.com/-/user_settings/personal_access_tokens).
2. Select Add new token
3. In the token creation form:
    1. pick a descriptive name for the token
    2. pick an expiration date if needed
    3. select the `api` scope
4. After you have a token, enter it into the prompt.

More Info: [Authentication - Gitlab Personal Access Token](https://abhinav.github.io/git-spice/setup/auth/#personal-access-token)

## Setting up a Github Classic Token

With classic tokens, you can grant access to all repositories, or all public repositories only. These tokens have the ability to never expire.

To use a classic token:

1. Go to [https://github.com/settings/tokens/new](https://github.com/settings/tokens/new). This may ask you to re-authenticate.
2. In the token creation form:
    1. enter a descriptive note for the token
    2. pick an expiration window, or select "No expiration"
    3. select `repo` scope for full access to all repositories, or `public_repo` for access to public repositories only
    4. Click "Generate token" and copy the token.
3. After you have a token, enter it into the prompt.

More info: [Authentication - Github Classic Token](https://abhinav.github.io/git-spice/setup/auth/#classic-token)

## Bypassing invalid certificates

If using a self-signed or expired certifiate at a private Github or Gitlab instance, prefix the `gs` command location to the stored certificate to trust:

```bash
SSL_CERT_FILE=/path/to/trusted/cert.crt gs branch submit --publish
```

The cert can be downloaded with openssl:

```bash
openssl s_client -showcerts -connect github.example.com:443 < /dev/null | openssl x509 -outform PEM > server_certificate.pem
```

## References

* [git-spice Website](https://abhinav.github.io/git-spice/)
* [git-spice source | Github](https://github.com/abhinav/git-spice)
