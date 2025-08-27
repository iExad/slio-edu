# Start by building the application.
FROM golang:1.19-alpine as build

WORKDIR /go/src/app
COPY . .

RUN go mod download
RUN go build -o /go/bin/app.bin cmd/main.go

FROM alpine:latest
WORKDIR /go

COPY --from=build /go/bin/app.bin .

RUN adduser -D dev && mkdir /upload && ln -s /upload ./uploads && chown -R dev:dev /go && chown dev:dev /upload

VOLUME /upload
EXPOSE 9999
USER dev
ENTRYPOINT ["/go/app.bin"]