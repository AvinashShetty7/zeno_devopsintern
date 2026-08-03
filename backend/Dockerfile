# Stage 1 - Build
FROM node:20-alpine AS build

WORKDIR /app

# Copy package files first for better layer caching
COPY package*.json ./

# Install all dependencies (including devDependencies)
RUN npm install

# Copy source code
COPY . .

# Stage 2 - Production
FROM node:20-alpine

WORKDIR /app

# Copy package files
COPY --from=build /app/package*.json ./

# Install only production dependencies
RUN npm install --omit=dev

# Copy application source
COPY --from=build /app .

EXPOSE 8000

CMD ["node", "server.js"]