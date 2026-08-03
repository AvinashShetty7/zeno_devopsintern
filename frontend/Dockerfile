# ---------- Stage 1: Build React Application ----------
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy application source code
COPY . .

# Build-time environment variable (optional)
# ARG VITE_API_URL=http://your-api-url
# ENV VITE_API_URL=${VITE_API_URL}

# Build the React application
RUN npm run build


# ---------- Stage 2: Serve with Nginx ----------
FROM nginx:alpine

# Copy the built React files to the Nginx web root
COPY --from=build /app/dist/ /usr/share/nginx/html/

# Expose HTTP port
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]