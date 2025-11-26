## Demo 001 - encrypt with a key, decrypt with another

See [`demo-001`](../demo-001) for basic usage

```sh
nix develop
cd demo-002
age-keygen -o demo-key-1.txt # note: this is a demo! don't actually commit this in your project!
age-keygen -o demo-key-2.txt # note: this is a demo! don't actually commit this in your project!
export SOPS_AGE_KEY_FILE=$(pwd)/demo-key-1.txt
export SOPS_AGE_KEY=age16gktgzcp4z3l6sew3vdgtp4gd4m98ck5atkdgaumpjda5fv0npvsuaz53t
sops edit my-shared-secrets.json
```

Let's verify that we can't read secrets without the key:

```sh
unset SOPS_AGE_KEY_FILE
unset SOPS_AGE_KEY
sops decrypt my-shared-secrets.json
```

Let's use the second key to read secrets:

```sh
export SOPS_AGE_KEY_FILE=$(pwd)/demo-key-2.txt
export SOPS_AGE_KEY=age14v4dznhwv2eyu6r0dyl24q8knvrmefklz854mugrjewz84egmg0q43khk6
sops decrypt my-shared-secrets.json
```