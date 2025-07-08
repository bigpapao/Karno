# Multi-stage build for React app

# Build stage
FROM node:18-alpine as build

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --silent

# Copy source code
COPY . .

# Build arguments
ARG REACT_APP_API_URL
ARG REACT_APP_STRIPE_PUBLIC_KEY
ARG REACT_APP_GOOGLE_ANALYTICS_ID

# Set environment variables
ENV REACT_APP_API_URL=$REACT_APP_API_URL
ENV REACT_APP_STRIPE_PUBLIC_KEY=$REACT_APP_STRIPE_PUBLIC_KEY
ENV REACT_APP_GOOGLE_ANALYTICS_ID=$REACT_APP_GOOGLE_ANALYTICS_ID
ENV GENERATE_SOURCEMAP=false

# Build the application
RUN npm run build

# Production stage
FROM nginx:alpine

# Install curl for health checks
RUN apk add --no-cache curl

# Copy built app from build stage
COPY --from=build /app/build /usr/share/nginx/html

# Copy nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Create non-root user
RUN addgroup -g 1001 -S karno && \
    adduser -S karno -u 1001 -G karno

# Change ownership of nginx directories
RUN chown -R karno:karno /var/cache/nginx && \
    chown -R karno:karno /var/log/nginx && \
    chown -R karno:karno /etc/nginx/conf.d

# Change ownership of html directory
RUN chown -R karno:karno /usr/share/nginx/html

# Make nginx run as non-root user
RUN touch /var/run/nginx.pid && \
    chown -R karno:karno /var/run/nginx.pid

# Switch to non-root user
USER karno

# Expose port
EXPOSE 80

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:80 || exit 1

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
