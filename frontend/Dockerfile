# -------- Builder stage --------
FROM node:18-alpine AS builder
WORKDIR /app
COPY package.json frontend/package-lock.json* ./ 
RUN npm install

COPY . .
RUN npm run build

# -------- Final stage --------
FROM node:18-alpine
WORKDIR /app

ENV NODE_ENV=production
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./package.json
Copy --from=builder /app/.env.local ./.env.sample

EXPOSE 3000
CMD ["npm", "start"]
