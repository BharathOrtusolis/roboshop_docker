# ----------------------------
# Stage 1 - Build
# ----------------------------
FROM node:20-alpine3.22 AS builder

WORKDIR /opt/server

# Copy package files
COPY package*.json ./

# Install production dependencies
RUN npm install --omit=dev

# Copy application source
COPY . .

# ----------------------------
# Stage 2 - Runtime
# ----------------------------
FROM node:20-alpine3.22

# Create non-root user
RUN addgroup -S roboshop && \
    adduser -S roboshop -G roboshop

# Set working directory
WORKDIR /opt/server

# Copy application from builder
COPY --from=builder --chown=roboshop:roboshop /opt/server /opt/server

# Environment variables
ENV MONGO=true \
    MONGO_URL=mongodb://mongodb:27017/catalogue

# Run as non-root user
USER roboshop

# Start application
CMD ["node", "server.js"]