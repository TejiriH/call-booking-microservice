# Use a slim Node.js image for building the React app
FROM node:18-slim AS builder

# Set the working directory
WORKDIR /app

# Copy package files first to leverage Docker layer caching
COPY package*.json ./

# Install dependencies
RUN npm install --omit=dev

# Copy all source code
COPY . .

# Build the React application
RUN npm run build

# Use a lightweight Nginx image for serving the built app
FROM nginx:alpine

# Create a non-root user for better security
RUN adduser -D -u 1001 adminui

# Set working directory and assign ownership
WORKDIR /usr/share/nginx/html
RUN chown -R adminui:adminui /usr/share/nginx/html /home

# Copy built files from the builder stage (Fix path issue)
COPY --from=builder /app/build /usr/share/nginx/html

# Copy custom Nginx config if needed
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Set correct permissions
RUN chmod -R 755 /usr/share/nginx/html

# Expose the correct port for Nginx
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

