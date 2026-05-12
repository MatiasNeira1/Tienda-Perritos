FROM node:18-alpine AS builder

WORKDIR /app


COPY package*.json ./


RUN npm install --production

COPY . .

# ==========================================
FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/ ./


USER node


EXPOSE 3001

CMD ["npm", "start"]