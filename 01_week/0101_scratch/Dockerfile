# Start by building the application.
FROM golang:1.19-alpine as build

WORKDIR /go/src/app
COPY . .

RUN go mod download
RUN go build -o /go/bin/app.bin cmd/main.go

FROM alpine:latest
WORKDIR /go

COPY --from=build /go/bin/app.bin .
VOLUME /upload
RUN adduser -D dev && mkdir ./uploads && chown -R dev:dev /go

EXPOSE 9999
USER dev
ENTRYPOINT ["/go/app.bin"]