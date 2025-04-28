# ---------------- Stage 1: Build Stage ----------------
FROM node:21 AS frontend-builder

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies (ignore peer deps issues)
RUN npm install --legacy-peer-deps

# Copy the rest of the application code
COPY . .

# ---------------- Stage 2: Final Stage ----------------
FROM node:21-slim

# Set the working directory to /app
WORKDIR /app

# Copy built assets and dependencies from frontend-builder stage
COPY --from=frontend-builder /app .

# Copy the .env.docker file to .env.local (optional if you have environment variables)
COPY .env.docker .env.local

# Install production dependencies only (optional, if your app needs)
# RUN npm ci --only=production

# Expose the frontend port (adjust if needed)
EXPOSE 5173

# Start the frontend application
CMD ["npm", "run", "dev"]
