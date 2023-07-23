FROM node:18-alpine AS base

FROM base AS builder
# Check https://github.com/nodejs/docker-node/tree/b4117f9333da4138b03a546ec926ef50a31506c3#nodealpine to understand why libc6-compat might be needed.
RUN apk add --no-cache libc6-compat
RUN apk update
# Set working directory
WORKDIR /app
RUN npm i -g pnpm
COPY . .
RUN pnpx turbo prune --scope=home --scope=shared --docker

RUN pnpm install

# Build the project
COPY turbo.json turbo.json

RUN yarn turbo run build --filter=home...

CMD pnpm dev  --filter=home...
