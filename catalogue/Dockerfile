FROM node:20-alpine3.12

# Create a non-root user and group
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

# Set working directory
WORKDIR /opt/server

# Copy package files
COPY package*.json ./

# Change ownership
RUN chown -R roboshop:roboshop /opt/server

# Switch to non-root user
USER roboshop

# Install dependencies
RUN npm install

# Copy application source
COPY --chown=roboshop:roboshop . .

# Environment variables
ENV MONGO=true \
    MONGO_URL=mongodb://mongodb:27017/catalogue

# Start application
CMD ["node", "server.js"]