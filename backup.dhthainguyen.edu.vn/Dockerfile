# Stage 1: Build
FROM node:18-alpine AS builder
#
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
# Stage 2: Run 
FROM node:18-alpine
RUN addgroup -S -g 1001 appgroup && \
    adduser -S -u 1001 -G appgroup appuser
WORKDIR /app
COPY --from=builder --chown=appuser:appgroup /app ./

# Tạo thư mục cache và cấp quyền
RUN mkdir -p /app/.next/cache/images && \
    chown -R appuser:appgroup /app/.next/cache

USER appuser
EXPOSE 3000
CMD ["npm", "start"]
