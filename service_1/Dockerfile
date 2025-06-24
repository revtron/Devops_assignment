# Use a minimal Go image
FROM golang:1.23-alpine

# Set the working directory
WORKDIR /app

# Install curl for healthcheck
RUN apk add --no-cache curl

# Copy all files from the host to the container
COPY . .

# Build the Go application
RUN go build -o main .

# Expose the service port
EXPOSE 8001

# Run the compiled Go app
CMD ["./main"]


HEALTHCHECK --interval=10s --timeout=5s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8001/ping || exit 1




































