FROM golang:1.17 AS builder

WORKDIR /app

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main ./cmd/api/

FROM alpine:latest AS application
#переписать команду добавление юзера
RUN adduser -D -h /home/admin -s /bin/bash -G root -u 1001 admin

USER admin

WORKDIR /home/admin

COPY --from=builder /app/main .

EXPOSE 8080

CMD ["./main"]

