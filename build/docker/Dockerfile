FROM alpine as certs
RUN apk update && apk add ca-certificates

FROM busybox
COPY --from=certs /etc/ssl/certs /etc/ssl/certs
COPY vocechat-server /home/vocechat-server/vocechat-server
COPY config /home/vocechat-server/config
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ARG GNOMCHAT_BUILD_SHA=dev
ENV VOCECHAT_FCM_PROJECT_ID=""\
    VOCECHAT_FCM_PRIVATE_KEY=""\
    VOCECHAT_FCM_CLIENT_EMAIL=""\
    VOCECHAT_FCM_TOKEN_URI="https://oauth2.googleapis.com/token"\
    GNOMCHAT_BUILD_SHA="${GNOMCHAT_BUILD_SHA}"
EXPOSE 3000
WORKDIR /home/vocechat-server
ENTRYPOINT ["/docker-entrypoint.sh"]
