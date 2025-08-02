FROM node:18 AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci --only=production && \
    npm audit fix
COPY . ./

FROM gcr.io/distroless/nodejs24-debian12 AS production
WORKDIR /app
COPY --from=builder /app ./
EXPOSE 5001
CMD ["src/index.js"]
