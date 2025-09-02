FROM golang:1.17 as build-stage

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main ./cmd/api/

FROM alpine:latest as production-stage

RUN adduser -D -u 1001 admin

USER admin

WORKDIR /home/admin

COPY --from=build-stage /app/main .

EXPOSE 8081

CMD ["./main"]

