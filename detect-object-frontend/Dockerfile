# Base image for Node.js environment
FROM node:21.7.3-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package.json and yarn.lock
COPY package*.json yarn.lock ./

# Install dependencies
RUN yarn install --frozen-lockfile

# Copy the rest of the project files (including the public directory)
COPY . .

# Build the application
RUN yarn build

# Base image for serving the React application
FROM nginx:alpine

# Set working directory
WORKDIR /usr/share/nginx/html

# Remove default Nginx static assets
RUN rm -rf ./*

# Copy the build output from the builder stage
COPY --from=builder /app/build .

# Expose port for the application
EXPOSE 3000

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

