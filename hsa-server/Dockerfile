FROM node:16 AS BUILD_IMAGE

RUN curl -sf https://gobinaries.com/tj/node-prune | sh

WORKDIR /app

COPY . /app

EXPOSE 8060

RUN npm install && npm run build

# remove development dependencies
  RUN npm prune --production

# run node prune
RUN /usr/local/bin/node-prune

FROM node:16-alpine

WORKDIR /app

# copy from build image
COPY --from=BUILD_IMAGE /app/dist ./dist
COPY --from=BUILD_IMAGE /app/node_modules ./node_modules

CMD node dist/index.js