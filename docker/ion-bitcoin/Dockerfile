FROM node:14.16.0-buster-slim as builder

WORKDIR /ion

COPY package.json package-lock.json ./

RUN npm install

COPY . .

FROM node:14.16.0-buster-slim as final

ARG USER=ion

COPY --from=builder --chown=$USER:$USER /ion /ion

RUN adduser --no-create-home --shell /bin/bash --disabled-login --gecos "$USER user" $USER

COPY ./docker/ion-bitcoin/entrypoint.sh /entrypoint.sh

RUN chown $USER:$USER /entrypoint.sh && \
    chmod u+x /entrypoint.sh && \
    chmod g+x /entrypoint.sh

USER $USER

ENTRYPOINT [ "/entrypoint.sh" ]