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