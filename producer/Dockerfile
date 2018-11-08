FROM golang:1.8.1-alpine as builder

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/streadway/amqp

ENV SOURCES /go/src/github.com/ciaranRoche/rabbitmq-docker/
COPY . ${SOURCES}

RUN cd ${SOURCES}/producer/ && CGO_ENABLED=0 go build

ENV BROKER_ADDR amqp://guest:guest@localhost:5672/

FROM scratch 
ENV BROKER_ADDR amqp://guest:guest@localhost:5672/
COPY --from=builder /go/src/github.com/ciaranRoche/rabbitmq-docker/producer/producer /go/src/github.com/ciaranRoche/rabbitmq-docker/producer/producer

ENTRYPOINT [ "/go/src/github.com/ciaranRoche/rabbitmq-docker/producer/producer" ]

