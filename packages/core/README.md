# @drift/core

The core framework package for Drift - High-Performance Node.js Framework.

## Installation

```bash
npm install drift
# or
pnpm add drift
```

## Features

- **HTTP Server** - Native Node.js HTTP/HTTP2 server
- **Radix Tree Router** - O(1) route lookup for blazing fast performance
- **Middleware Pipeline** - CORS, Helmet, Rate Limiting, JSON, Query parsing
- **Dependency Injection** - Full DI container with auto-wiring
- **Decorator-based Routing** - NestJS-style decorators
- **Module System** - Organize your application into modules
- **Schema Validation** - Built-in Zod integration
- **Logging** - Pino logger integration

## Quick Start

```typescript
import { Drift, cors, Controller, Get } from 'drift';

@Controller('/api')
class UserController {
  @Get('/users')
  getUsers(_req: any, res: any) {
    res.json({ users: [] });
  }
}

const app = new Drift({ port: 3000, logger: true });
app.use(cors());
app.get('/', (_req, res) => res.json({ hello: 'world' }));

await app.listen();
```

## Decorators

### Controller
```typescript
@Controller('/api')
class ApiController {}
```

### Route Methods
```typescript
@Get('/users')
@Post('/users')
@Put('/users/:id')
@Delete('/users/:id')
@Patch('/users/:id')
@Options('/users')
@Head('/users')
@All('/users') // All methods
```

### DI
```typescript
@Injectable()
class UserService {
  getUsers() { return []; }
}

@Controller('/users')
class UserController {
  constructor(private userService: UserService) {}
}
```

## Middleware

```typescript
import { cors, helmet, rateLimit, json, query, logger } from 'drift';

app.use(cors());
app.use(helmet());
app.use(rateLimit({ max: 100, windowMs: 60000 }));
app.use(json());
app.use(query());
app.use(logger(myLogger));
```

## Vercel Adapter

```typescript
import { Drift, toVercel } from 'drift';

const app = new Drift();
app.get('/', (_req, res) => res.json({ hello: 'world' }));

export default toVercel(app);
```

## License

Apache 2.0 - See [LICENSE](../LICENSE)
