# Stage 1: Build the Go app
FROM golang:1.23.2-alpine as builder

# Set working directory
WORKDIR /app

# Copy go.mod and go.sum to download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN go build -o main .

# Stage 2: Run the Go app in a lightweight container
FROM alpine:latest

# Copy the binary from the builder stage
COPY --from=builder /app/main /app/main

# Expose the port your application will run on (adjust as needed)
EXPOSE 8080

# Run the Go app
CMD ["/app/main"]
