FROM node:20 AS Build

WORKDIR /build

EXPOSE 443
EXPOSE 80

ENV NUXT_HOST=0.0.0.0
ENV PORT=80

RUN npm install -g pnpm@10
COPY pnpm-lock.yaml ./

ADD . ./
RUN pnpm install

# The release workflow passes the release version, which the frontend reports as its client version.
ARG APP_VERSION=
RUN if [ -n "$APP_VERSION" ]; then npm version "$APP_VERSION" --no-git-tag-version --allow-same-version; fi

RUN pnpm run build

ENTRYPOINT ["pnpm", "run", "start"]
