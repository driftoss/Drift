# @drift/microservices

Microservices module for Drift Framework.

## Installation

```bash
npm install drift-microservices
# or
pnpm add drift-microservices
```

## Features

- **TCP Transport** - Low-latency socket communication
- **HTTP Transport** - REST-based inter-service communication
- **Service Registry** - Service discovery and health checks
- **Redis Pub/Sub** - Event-driven communication
- **Redis Cache** - Distributed caching
- **API Gateway** - Single entry point for microservices

## Quick Start

### TCP Microservice

```typescript
import { MicroserviceServer } from 'drift-microservices';

const server = new MicroserviceServer({
  port: 3001,
  name: 'user-service'
});

server.registerHandler('users:find', async (msg) => {
  return { id: msg.data.id, name: 'John' };
});

await server.listen();
```

### TCP Client

```typescript
import { MicroserviceClient } from 'drift-microservices';

const client = new MicroserviceClient('localhost', 3001);
await client.connect();

const result = await client.sendMessage('users:find', { id: 1 });
console.log(result);
```

### Service Registry

```typescript
import { ServiceRegistry } from 'drift-microservices';

const registry = new ServiceRegistry();

// Register a service
registry.register({
  name: 'user-service',
  host: 'localhost',
  port: 3001
});

// Discover services
const instances = registry.find('user-service');
const instance = registry.findOne('user-service');
```

### Redis Pub/Sub

```typescript
import { RedisPubSub } from 'drift-microservices';

const pubsub = new RedisPubSub({ host: 'localhost', port: 6379 });
await pubsub.connect();

// Subscribe to events
await pubsub.subscribe('user:created', (data) => {
  console.log('User created:', data);
});

// Publish events
await pubsub.publish('user:created', { id: 1, name: 'John' });
```

### API Gateway

```typescript
import { APIGateway, ServiceRegistry } from 'drift-microservices';

const registry = new ServiceRegistry();
registry.register({ name: 'user-service', host: 'localhost', port: 3001 });

const gateway = new APIGateway({
  port: 8080,
  routes: [
    { path: '/api/users/*', service: 'user-service' }
  ]
}, registry);

await gateway.listen();
```

## License

Apache 2.0 - See [LICENSE](../LICENSE)
