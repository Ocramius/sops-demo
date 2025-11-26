## Demo 001 - encrypt with a key, decrypt with another

See [`demo-001`](../demo-001) for basic usage

```sh
nix develop
cd demo-004
age-keygen -o demo-key-1.txt
export SOPS_AGE_KEY_FILE=$(pwd)/demo-key-1.txt
export SOPS_AGE_KEY=age1unuh3fnddthjd9d58zr72zqfrpg0efnnfh62477av3szpz0733yqt69wwk
sops my-re-encrypted-secret.json
```

Now let's add a new key:

```sh
age-keygen -o demo-key-2.txt
```

Edit `.sops.yaml` to add the new key

```sh
sops updatekeys my-re-encrypted-secret.json
```

Let's use the second key to read secrets:

```sh
export SOPS_AGE_KEY_FILE=$(pwd)/demo-key-1.txt
export SOPS_AGE_KEY=age1unuh3fnddthjd9d58zr72zqfrpg0efnnfh62477av3szpz0733yqt69wwk
sops decrypt my-re-encrypted-secret.json
```