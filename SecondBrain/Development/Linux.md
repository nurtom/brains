## Create an public private key and add public key to authorized_keys

Current algorithm with elliptic curves

```bash
ssh-keygen -t rsa -b 4096 -C "Gitlab CI Pipeline" -f ./id_rsa
```

Old RSA algorithm

```bash
ssh-keygen -t ed25519 -C "Gitlab CI Pipeline" -f ./id_ed25519
```

## show firewall rules

```bash
nft list rulesset
```

## Test harddisk

```bash
sudo badblocks -b 4096 -sv -wt random /dev/sd
```