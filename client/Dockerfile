FROM node:18-alpine as build
WORKDIR /app
COPY package*.json ./ 
RUN npm install
COPY . .
RUN npm run build

###### 2nd ####

FROM nginx:alpine
# ADD THIS LINE TO BREAK THE CACHE:
ENV REFRESHED_AT=2025-12-11
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

RUN echo "--- CHECKING CONFIG FILE CONTENT ---" && \
    cat /etc/nginx/conf.d/default.conf && \
    echo "--- END CHECK ---"
EXPOSE 80
CMD [ "nginx","-g","daemon off;" ]
