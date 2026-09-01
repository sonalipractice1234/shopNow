FROM node:18-alpine

WORKDIR /app

# Install production dependencies
COPY package*.json ./
RUN npm ci --omit=dev --no-audit --prefer-offline

# Copy application source
COPY . .

# Create non-root user with numeric UID
RUN addgroup -S appgroup -g 1001 && \
    adduser -S appuser -u 1001 -G appgroup

# Give ownership to non-root user
RUN chown -R 1001:1001 /app

# Run as numeric non-root user
USER 1001

ENV NODE_ENV=production
ENV PORT=5000

EXPOSE 5000

CMD ["npm", "start"]
