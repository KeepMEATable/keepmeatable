FROM alpine:latest

RUN apk update && apk add --no-cache openssl

COPY ssl.conf /tmp/ssl.conf

# Use this self-generated certificate only in dev, IT IS NOT SECURE!
RUN openssl genrsa -des3 -passout pass:NotSecure -out localhost.pass.key 2048
RUN openssl rsa -passin pass:NotSecure -in localhost.pass.key -out localhost.key
RUN rm localhost.pass.key
RUN openssl req -x509 -out localhost.crt -keyout localhost.key \
      -newkey rsa:2048 -nodes -sha256 \
      -subj '/CN=*.keepmeatable.dev' \
      -extensions EXT \
      -config /tmp/ssl.conf

FROM nginx:1.15-alpine

RUN apk update && apk add --no-cache ca-certificates

RUN mkdir -p /etc/nginx/certs/
COPY --from=0 localhost.key localhost.crt /etc/nginx/certs/
COPY --from=0 localhost.crt /usr/share/ca-certificates/
COPY conf.d /etc/nginx/conf.d/
