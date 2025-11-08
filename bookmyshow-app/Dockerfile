# Use a modern, stable Node base image
FROM node:20-bullseye

# Set working directory
WORKDIR /app

# Copy dependency files first (to leverage Docker cache)
COPY package*.json package-lock.json ./

# Update npm to a stable version compatible with PostCSS
RUN npm install -g npm@10.8.2

# Clean npm cache to avoid corrupted cache layers
RUN npm cache clean --force

# Install PostCSS and safe parser before main dependencies
RUN npm install postcss@8.4.21 postcss-safe-parser@6.0.0 --legacy-peer-deps

# Install project dependencies
RUN npm install --legacy-peer-deps

# Copy the rest of the application code
COPY . .

# Expose the port
EXPOSE 3000

# Environment setup to avoid OpenSSL issues
ENV NODE_OPTIONS=--openssl-legacy-provider
ENV PORT=3000

# Run the app
CMD ["npm", "start"]

