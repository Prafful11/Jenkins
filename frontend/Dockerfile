# ---------------- Stage 1: Build Stage ----------------
FROM node:21 AS frontend-builder

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies (skip peer dependency errors + ignore lifecycle scripts)
RUN npm install --legacy-peer-deps --ignore-scripts

# Copy the rest of the application code
COPY . .

# ---------------- Stage 2: Final Stage ----------------
FROM node:21-slim

# Set the working directory to /app
WORKDIR /app

# Copy built assets and dependencies from frontend-builder stage
COPY --from=frontend-builder /app .

# Copy the .env.docker file to .env.local (must exist in frontend root)
COPY .env.docker .env.local

# Expose the frontend port (Vite default is 5173)
EXPOSE 5173

# Start the frontend application
CMD ["npm", "run", "dev"]
