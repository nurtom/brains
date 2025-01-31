## Create random password/string
#openssl #password

16 Bytes ergibt 32 chars (Achtung: nur HEX Alphabet)

```bash
openssl rand -hex 16
```

## Create asymmetric encryption key pair
#openssl #certificates

Create a private key

```bash
openssl genrsa -out rsa_4096_priv.pem 4096
```

Create a private key with password

```bash
openssl genrsa -aes256 -out rsa_4096_priv.pem 4096
```

Create a public Key from above private key

```bash
openssl rsa -pubout -in rsa_4096_priv.pem -out rsa_4096_pub.pem
```

## add ssh public key

```bash
cd ~
mkdir .ssh && chmod 0700 .ssh
cd .ssh && touch authorized_keys && chmod 0600 authorized_keys
```