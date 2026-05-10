# ==========================================
# Etapa 1: Construcción (Builder)
# ==========================================
FROM node:18-alpine AS builder

WORKDIR /app

# Copiamos solo los archivos de dependencias primero para aprovechar la caché de Docker
COPY package*.json ./

# Instalamos las dependencias
RUN npm install --production

# Copiamos el resto del código del backend
COPY . .

# ==========================================
# Etapa 2: Producción (Imagen ligera)
# ==========================================
FROM node:18-alpine

WORKDIR /app

# Copiamos desde la etapa 'builder' solo lo necesario
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/ ./

# APLICANDO MÍNIMO PRIVILEGIO: Cambiamos al usuario 'node' (no root)
USER node

# Exponemos el puerto de tu backend
EXPOSE 3001

CMD ["npm", "start"]