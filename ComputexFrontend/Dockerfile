# Stage 1: Build the Vite React app
FROM node:18 AS build
WORKDIR /app

# Copy only package files first (for better caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the project files
COPY . .

# Build the production bundle
RUN npm run build

# Stage 2: Serve the build with nginx
FROM nginx:alpine

# Copy Vite build output (from /app/dist) to Nginx web root
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

