# Stage 1: Build the Node.js application
FROM node:18-alpine AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build or do other necessary tasks, if any

# Stage 2: Set up Nginx to serve the app
FROM nginx:alpine

# Copy Nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Copy static assets from Node.js build (adjust paths based on your app)
COPY --from=build /app/app/public /usr/share/nginx/html

# Copy Node.js app to the container
COPY --from=build /app /usr/src/app

# Install Node.js in this stage too (so that Node.js is available for your app)
RUN apk add --no-cache nodejs npm

# Set working directory for Node.js
WORKDIR /usr/src/app

# Expose necessary ports
EXPOSE 80 3005

# Command to start Nginx and Node.js
CMD ["sh", "-c", "nginx && node app.js"]

