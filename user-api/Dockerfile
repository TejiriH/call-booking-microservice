# Use a slim Node.js image for a smaller footprint
FROM node:17.4.0-slim

# Set a maintainer label
LABEL maintainer="Tejiri-DevOps"

# Create a non-root user for security
RUN useradd userapi

# Set working directory and ensure correct ownership
WORKDIR /app
RUN chown -R userapi:userapi /app /home

# Copy package files first to optimize Docker layer caching
COPY package*.json ./

# Install dependencies
RUN npm install --omit=dev

# Copy remaining files
COPY . .

# Expose the application port
EXPOSE 1004

# Set default environment variables (can be overridden at runtime)
ENV MONGO_URL="" \
    ADMIN_EMAIL=""

# Switch to non-root user
USER userapi

# Start the application
CMD ["npm", "start"]
