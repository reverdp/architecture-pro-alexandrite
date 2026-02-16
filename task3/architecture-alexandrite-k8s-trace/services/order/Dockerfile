FROM golang:1.24.6 AS build
WORKDIR /src

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /app/order .

FROM gcr.io/distroless/static:nonroot
COPY --from=build /app/order /order
USER nonroot:nonroot

EXPOSE 8080
ENTRYPOINT ["/order"]
