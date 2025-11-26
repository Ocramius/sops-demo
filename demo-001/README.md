## Demo 001 - simple encryption

```sh
nix develop
cd demo-001
age-keygen -o demo-key-1.txt # note: this is a demo! don't actually commit this in your project!
```

Now edit `.sops.yaml`: see https://github.com/getsops/sops#creation-rule-object
Be aware that `.sops.yaml` only contains public keys!

Let's then interact with our secrets:

```sh
export SOPS_AGE_KEY_FILE=$(pwd)/demo-key-1.txt
export SOPS_AGE_KEY=age19ztc06r746z79lqu8ns0jj2sx84a4nqd8n4crqvjzfq8hrqmr4wqud9r9k
sops edit my-secrets.json
```

Secrets should now be encrypted:

```sh
cat my-secrets.json
```

Secrets can be interacted with as long as the private key for decryption is available:

```sh
sops edit my-secrets.json
unset SOPS_AGE_KEY_FILE
unset SOPS_AGE_KEY
sops edit my-secrets.json # will fail
```