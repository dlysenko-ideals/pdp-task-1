FROM node:24.1.0-bullseye AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:1.28-alpine AS final
RUN addgroup -S nonroot && adduser -S nonroot -G nonroot
COPY docker/default.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/pdp-task-1/browser /usr/share/nginx/html
RUN chown -R nonroot:nonroot /usr/share/nginx/html
EXPOSE 80