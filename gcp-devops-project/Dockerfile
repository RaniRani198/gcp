# Use the official Node.js image
FROM node:14

# Set the working directory
WORKDIR /app

# Copy package files and install dependencies
COPY app/package*.json ./
RUN npm install

# Copy application source code
COPY app/ .

# Expose the application port
EXPOSE 8080

# Start the app
CMD ["node", "server.js"]
