# syntax=docker/dockerfile:1

FROM node:22-alpine AS deps
WORKDIR /app
COPY package.json yarn.lock ./
RUN node -e "const fs = require('fs'); const pkg = require('./package.json'); delete pkg.dependencies.sqlite3; fs.writeFileSync('package.json', JSON.stringify(pkg, null, 2));" \
    && yarn install --production --frozen-lockfile

FROM node:22-alpine
WORKDIR /app
ENV NODE_ENV=production
COPY --from=deps /app/node_modules ./node_modules
COPY . .
CMD ["node", "src/index.js"]
EXPOSE 3000
