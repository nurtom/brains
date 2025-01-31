#nodejs #nvm #proxy 

Set bash proxy for the install scripts.

```bash
set HTTP_PROXY=http://10.9.53.100:3128/
set HTTPS_PROXY=http://10.9.53.100:3128/
```

Follow the [official installation instructions](https://nodejs.org/en/download/package-manager)

> [!warning]
> Adapt to the current version number of the script!

e.g.:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

Set the proxy for curl in ```~/.curlrc``` to be able to download nodejs versions

```
proxy = http://10.9.53.100:3128/
```

Check available versios and install and use a nodejs version e.g.

```bash
nvm ls-remote
nvm install 20
node -v
npm -v
```

Use proxy for npm installs

```bash
npm config set proxy http://10.9.53.100:3128/
npm config set https-proxy http://10.9.53.100:3128/
```


