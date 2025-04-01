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

COPY nginx.conf /etc/nginx/conf.d/default.conf


# Copy built files from the builder stage
COPY --from=builder /app/build /usr/share/nginx/html

# Expose the correct port for Nginx
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]


