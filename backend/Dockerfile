FROM golang:1.17 AS builder

WORKDIR /app

COPY . .

RUN go build -o main .

FROM alpine:latest AS application

RUN adduser -D -h /home/admin -s /bin/bash -G root -u 1001 admin && \
    adduser admin sudo

USER admin

WORKDIR /home/admin

COPY --from=builder /app/main .

CMD ["./main"]

