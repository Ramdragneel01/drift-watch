FROM cgr.dev/chainguard/node:latest-dev AS build

WORKDIR /app

COPY package.json ./package.json
RUN npm install

COPY . .
RUN npm run build

FROM cgr.dev/chainguard/node:latest

WORKDIR /app

COPY --from=build /app/dist ./dist
COPY server.mjs ./server.mjs

EXPOSE 8080

CMD ["node", "server.mjs"]
