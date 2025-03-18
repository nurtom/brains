## Create random password and corresponding hash
#brypt

Used for:
- send password to user
- save hash in database

```typescript
import { randomBytes } from "crypto";
import * as bcrypt from "bcryptjs";

const randomPassword = randomBytes(20).toString("hex");
const hash = await bcrypt.hash(randomPassword, 10);
```

## Extend jsonwebtoken payload Typescript type
#typescript

```typescript
import * as jwt from 'jsonwebtoken'

declare module 'jsonwebtoken' {
    export interface UserIDJwtPayload extends jwt.JwtPayload {
        userId: string
    }
}

export const userIdFromJWT = (jwtToken: string): string | undefined => {
    try {
        const { userId } = <jwt.UserIDJwtPayload>jwt.verify(jwtToken, process.env.JWT_COOKIE_SECRET || 'MISSING_SECRET')

        return userId
    } catch (error) {
        return undefined
    }
}
```

# React development

### Ensure file watcher is working
#react

```bash
cat /proc/sys/fs/inotify/max_user_watches
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
cat /proc/sys/fs/inotify/max_user_watches
```


## Vite: don't inline assets

Set ```assetsInlineLimit: 0``` in ```vite.config.ts```

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  build: {
    assetsInlineLimit: 0,
  },
});
```