# Use the official Node.js image
FROM node:20

# Set working directory inside the container
WORKDIR /usr/src/app

# Copy package files first for caching
COPY --chown=node:node package*.json ./

# Install dependencies
RUN npm ci

# Copy the rest of the app with proper ownership
COPY --chown=node:node . .

# Set environment variables for enabling debug logs
ENV DEBUG=playground:*

# Swtich to on-root usernode
USER node

# Expose port
EXPOSE 3000

# Default command

CMD ["npm", "start"]
