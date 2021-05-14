ARG DENO_VERSION=1.10.1
FROM openfaas/of-watchdog:0.7.7 as watchdog
FROM hayd/deno:alpine-${DENO_VERSION}

WORKDIR /root/

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog

ENV FUNC_HOME_DIR=/home/app
ENV FUNC_HANDLER_DIR=${FUNC_HOME_DIR}/function
ENV FUNC_LIB_DIR=${FUNC_HOME_DIR}/lib
ENV DENO_DIR=${FUNC_HOME_DIR}/.cache/deno

# Make function directory
# Install deno
# Set function user permissions
RUN mkdir -p ${FUNC_HANDLER_DIR} \
  && mkdir -p ${FUNC_LIB_DIR} \
  && mkdir -p ${DENO_DIR} \
  && chmod +x /usr/bin/fwatchdog \
  && apk --no-cache add ca-certificates \
  && addgroup -S -g 12000 fnGroup \
  && adduser -S --home ${FUNC_HOME_DIR} -u 12000 -g 12000 fnUser \
  && chown fnUser:fnGroup -R ${FUNC_HOME_DIR} \
  && chmod 777 /tmp

HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

# OpenFaaS vars
ENV cgi_headers="true"
ENV fprocess="deno run --allow-net --allow-env main.ts"
ENV mode="http"
ENV upstream_url="http://127.0.0.1:3000"
ENV exec_timeout="10s"
ENV write_timeout="15s"
ENV read_timeout="15s"
