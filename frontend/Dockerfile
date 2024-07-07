# stage 1: Build React application
FROM node:16-alpine as build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to work directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to work directory
COPY . .

# Build production bundle
RUN npm run build

# Stage 2: Serve the built React application with NGINX
FROM nginx:alpine

# Set working directory to nginx asset directory
WORKDIR /usr/share/nginx/html

# Remove default nginx static assets
RUN rm -rf ./*

# Copy static assets from builder stage
COPY --from=build /app/dist .

# Expose port 80
EXPOSE 80

# Command to start NGINX
CMD ["nginx", "-g", "daemon off;"]

