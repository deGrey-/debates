# Use Go base image
FROM golang:1.21 AS builder

WORKDIR /app

# Copy Go modules files first (to leverage Docker caching)
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the app
COPY . .

# Build the binary
RUN go build -o backend .

# Use a lightweight image for the final container
FROM alpine:latest

WORKDIR /root/

# Copy the built binary from the builder
COPY --from=builder /app/backend .

# Set permissions
RUN chmod +x ./backend

# Run the application
CMD ["./backend"]
