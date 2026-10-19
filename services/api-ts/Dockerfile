# The base image is pinned by digest as well as tag: a tag can be repointed at a different image.
# Dependabot updates both together.
FROM node:24-alpine@sha256:44fce696f38ba8c987c4db89954051000bbd05ffd8d8659ba15ed4a8602e937f
WORKDIR /app
ENV NODE_ENV=production
COPY package.json package-lock.json ./
# npm installs the dependencies, then leaves the image: nothing at runtime calls it, and the copy bundled
# with Node carries its own dependencies, with vulnerabilities of their own.
RUN npm ci --omit=dev --ignore-scripts \
    && rm -rf /usr/local/lib/node_modules/npm /usr/local/bin/npm /usr/local/bin/npx
# Node 24 runs TypeScript directly by stripping types, so the sources ship as they are.
COPY src ./src
USER node
EXPOSE 8080
CMD ["node", "src/main.ts"]
