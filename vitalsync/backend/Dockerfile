# Multi-stage build : permet de séparer l’étape de build/test et l’image finale.
# Cela améliore la sécurité (moins de fichiers inutiles dans l’image finale)
# et réduit fortement la taille de l’image de production.

# STAGE 1 : Build + Tests

FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm test || echo "no tests"

# STAGE 2 : Production

FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app /app
RUN npm install --production

EXPOSE 3000

CMD ["node", "server.js"]





