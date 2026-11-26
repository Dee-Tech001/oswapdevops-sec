# syntax=docker/dockerfile:1
FROM node:20-alpine AS builder
WORKDIR /app/frontend

COPY package*.json ./
RUN npm ci

COPY . .

# Default to relative /api so Nginx proxies to backend; override via --build-arg if needed
ARG VITE_API_URL=/api
ENV VITE_API_URL=$VITE_API_URL

RUN npm run build

FROM nginx:1.27-alpine AS runtime
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/frontend/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
