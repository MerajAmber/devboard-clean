FROM golang:tip-alpine3.24 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 go build -o devboard-backend .

FROM golang:tip-alpine3.24

WORKDIR /app

COPY --from=builder /app/devboard-backend ./devboard-backend

# Ensure binary is executable
# RUN chmod +x ./devboard-backend

EXPOSE 8080

# Use exec form for proper signal handling
ENTRYPOINT ["./devboard-backend"]
