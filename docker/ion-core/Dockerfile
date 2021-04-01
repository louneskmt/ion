FROM node:14.16.0-buster-slim as builder

WORKDIR /ion

COPY package.json package-lock.json ./

RUN npm install

COPY . .

RUN npm run build

FROM node:14.16.0-buster-slim as final

ARG USER=ion

RUN adduser --no-create-home --shell /bin/bash --disabled-login --gecos "$USER user" $USER

COPY --from=builder --chown=$USER:$USER /ion /ion

USER $USER

WORKDIR /ion

CMD [ "npm", "run", "core" ]