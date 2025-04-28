# Stage 1 - Build Stage
FROM node:21 AS backend-builder

# Set working directory
WORKDIR /app

# Copy source code
COPY . .

# Install dependencies
RUN npm install

# Stage 2 - Production Stage
FROM node:21-slim

# Set working directory
WORKDIR /app

# Copy compiled app from the previous stage
COPY --from=backend-builder /app .

# Copy environment-specific file
COPY .env.docker .env

# Expose port
EXPOSE 5000

# Start the app
CMD ["npm", "start"]
