ARG NODE_VERSION=16.14-alpine

FROM node:${NODE_VERSION} as node

FROM node as client-local-build

ARG APP_HOME=/app

WORKDIR ${APP_HOME}

COPY ./package*.json .

RUN npm install

COPY . ${APP_HOME}

# Change ownership of the entire /app directory to the node user
RUN chown -R node:node /app

CMD ["npm", "start"]
