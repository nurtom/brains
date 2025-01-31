#vscode #proxy 

Proxy needs to be set

```bash
set HTTP_PROXY=http://10.9.53.100:3128/
set HTTPS_PROXY=http://10.9.53.100:3128/
```

Check proxy setting

```bash
env
```

Go into a wsl folder and run 

```bash
code .
```

Add proxy within settings:

- got to File -> Preferences -> Settings
- search for Proxy
- set Http Proxy http://10.9.53.100:3128
- Disable Proxy Strict SSL
- Proxy Support: on
