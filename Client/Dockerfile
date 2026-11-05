FROM oven/bun:1 AS base

LABEL authors="G25"

WORKDIR /app

# Copy dependency definitions

COPY package.json bun.lock ./

# Install dependencies

RUN bun install --frozen-lockfile

# Copy application

COPY --chown=bun:bun . .

# Production configuration

ENV NODE_ENV=production
ENV PORT=3100

# Run as non-root user

USER bun

EXPOSE 3100

CMD ["bun", "run", "start"]
