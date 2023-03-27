FROM golang:1.19 as builder

WORKDIR /usr/src/fullcyclerocks

RUN go mod init example/fullcyclerocks

COPY fullcyclerocks.go .

RUN go build .

FROM hello-world:linux 

COPY --from=builder /usr/src/fullcyclerocks .

CMD ["./fullcyclerocks"]
