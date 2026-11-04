FROM oven/bun:1
LABEL authors="G25"
WORKDIR /app
COPY package.json bun.lock ./
RUN bun install --frozen-lockfile
COPY src ./src
ENV NODE_ENV=production
ENV PORT=3100
USER bun
EXPOSE 3100
CMD ["bun", "src/index.ts"]
