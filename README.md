# 🚀 Drift Framework

<p align="center">
  <strong>High-Performance Node.js Framework for Enterprise & Microservices</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/drift">
    <img src="https://img.shields.io/npm/v/drift" alt="npm version">
  </a>
  <a href="./LICENSE">
    <img src="https://img.shields.io/github/license/driftoss/Drift" alt="license">
  </a>
  <a href="https://github.com/driftoss/Drift/actions">
    <img src="https://img.shields.io/github/actions/workflow/status/driftoss/Drift/ci" alt="CI">
  </a>
</p>

---

## ✨ Features

- **⚡ Blazing Fast** - Radix Tree router for O(1) route lookup
- **🏢 Enterprise Ready** - Dependency Injection, Decorators, Modules
- **🌐 Microservices** - TCP/HTTP transport, Service Discovery, Redis Pub/Sub
- **🔒 TypeScript First** - Full type safety out of the box
- **📦 Modular** - Pay only for what you use
- **🛡️ Built-in Middleware** - CORS, Helmet, Rate Limiting, Validation
- **📝 Schema Validation** - Zod integration for request validation

---

## 📖 Quick Start

```bash
npm install drift
# or
pnpm add drift
# or
yarn add drift
```

```typescript
import 'reflect-metadata';
import { Drift, Controller, Get, cors } from 'drift';

@Controller('/api')
class UserController {
  @Get('/users')
  getUsers(_req: any, res: any) {
    res.json({ users: [{ id: 1, name: 'John' }] });
  }
}

const app = new Drift({ port: 3000, logger: true });
app.use(cors());
new Module({ controllers: [UserController] }).setupRoutes(app.getServer());

app.get('/', (_req, res) => res.json({ message: 'Hello!' }));

await app.listen();
```

---

## 🏗️ Architecture

```
drift/
├── packages/
│   ├── core/           # Main framework (HTTP, Router, DI, Middleware)
│   ├── microservices/  # Microservices module (TCP, HTTP, Redis, Gateway)
│   ├── utils/          # Utilities (Validation, etc.)
│   └── testing/        # Testing utilities
└── apps/
    └── playground/     # Demo application
```

---

## 📚 Modules

### Core (`drift`)
- HTTP Server with HTTP/2 support
- Radix Tree Router
- Middleware Pipeline
- Dependency Injection Container
- Decorator-based Routing
- Module System

### Microservices (`drift-microservices`)
- TCP Transport
- HTTP Transport
- Service Registry & Discovery
- Redis Pub/Sub
- API Gateway

---

## 🔧 Configuration

### Drift Options
```typescript
const app = new Drift({
  port: 3000,
  host: '0.0.0.0',
  http2: false,
  logger: true, // or custom pino logger
});
```

### Middleware
```typescript
import { cors, helmet, rateLimit, json, query } from 'drift';

app.use(cors());
app.use(helmet());
app.use(rateLimit({ max: 100, windowMs: 60000 }));
app.use(json());
app.use(query());
```

---

## 🧪 Testing

```bash
# Install dependencies
pnpm install

# Build all packages
pnpm build

# Run tests
pnpm test

# Run playground
cd apps/playground && pnpm dev
```

---

## 📄 License

Apache License 2.0 - see [LICENSE](./LICENSE)

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 🌍 Community

- [GitHub](https://github.com/driftoss/Drift)
- [GitHub Discussions](https://github.com/driftoss/Drift/discussions)
