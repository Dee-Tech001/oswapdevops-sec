
FROM node:20-alpine AS deps
WORKDIR /app/backend

COPY package*.json ./
RUN npm ci --omit=dev && npm cache clean --force

FROM node:20-alpine AS runtime
WORKDIR /app/backend

ENV NODE_ENV=production
ENV PORT=5000

COPY --from=deps /app/backend/node_modules ./node_modules
COPY . .

USER node
EXPOSE 5000

CMD ["node", "server.js"]
