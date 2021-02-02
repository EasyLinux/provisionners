FROM alpine:3.12 AS Build

RUN apk add go git build-base
RUN mkdir /app
WORKDIR /app
RUN git clone https://github.com/EasyLinux/nfs-subdir-external-provisioner.git .
RUN go build -ldflags '-extldflags "-static"' ./cmd/nfs-subdir-external-provisioner/


FROM alpine:3.12
LABEL author="Serge NOEL"

COPY --from=Build /app/nfs-subdir-external-provisioner /nfs-subdir-external-provisioner
ENTRYPOINT ["/nfs-subdir-external-provisioner"]