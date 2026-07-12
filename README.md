# nestjs-messenger

A NestJS monorepo scaffold demonstrating a microservices architecture with RabbitMQ as the message broker between services.

## What's inside

- Nest CLI monorepo with two independent applications: `api` and `auth`, each with its own bootstrap, module, controller, and service.
- A shared `common` library (`libs/common`) exposing an `RmqModule` / `RmqService`, the shared connection layer intended for services to publish and consume messages over RabbitMQ.
- `docker-compose.yml` to run a local RabbitMQ instance (with the management UI) for development.

This is a foundation/reference project for the Nest monorepo + RabbitMQ pattern — the `api` and `auth` apps currently each expose a basic HTTP endpoint, and `RmqService` is a stub ready to be built out with actual queue publishing/consuming logic.

## Tech stack

- NestJS (monorepo mode: multiple apps + a shared library)
- RabbitMQ, via `amqp-connection-manager` and `amqplib`
- TypeScript
- Jest for unit/e2e tests

## Quickstart

```bash
yarn install

# copy env vars and adjust as needed
cp .env.example .env

# start RabbitMQ locally
docker compose up -d

# run an app in watch mode
yarn start:dev
```

Environment variables (see `.env.example`):

- `RABBITMQ_HOST` — host:port of the RabbitMQ broker
- `RABBITMQ_USER` / `RABBITMQ_PASS` — broker credentials
- `RABBITMQ_AUTH_QUEUE` — name of the queue used by the auth service

## Apps

- `apps/api` — HTTP entry point (gateway-style service).
- `apps/auth` — separate service, same basic shape as `api`.
- `libs/common` — shared RabbitMQ connection module used by both apps.

## Tests

```bash
yarn test        # unit tests
yarn test:e2e    # e2e tests
yarn test:cov    # coverage
```
