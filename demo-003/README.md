## Demo 001 - encrypt with a key, decrypt with another

See [`demo-001`](../demo-001) for basic usage

```sh
nix develop
cd demo-003
age-keygen -o demo-key-1.txt # note: this is a demo! don't actually commit this in your project!
age-keygen -o demo-key-2.txt # note: this is a demo! don't actually commit this in your project!
gpg --list-secret-keys # grab the public ID of your secret key here!
sops my-shared-age-and-gpg-secrets.json
```

Let's verify that we can't read secrets with our GPG key:

```sh
sops decrypt my-shared-age-and-gpg-secrets.json
```

Now run this either on a machine that does not have your GPG key, or after making your GPG key
unavailable on the current system:

```sh
sops decrypt my-shared-age-and-gpg-secrets.json
```

Let's use another second key to read secrets:

```sh
export SOPS_AGE_KEY_FILE=$(pwd)/demo-key-1.txt
export SOPS_AGE_KEY=age1c80m52d97ru0u7qmkx8umf5fhem5df8dnkjg6h8z6kfnke63894sevcrh2
sops decrypt my-shared-age-and-gpg-secrets.json
```