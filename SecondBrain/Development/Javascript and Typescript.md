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
