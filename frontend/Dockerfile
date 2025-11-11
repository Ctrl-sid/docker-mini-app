# Stage 1: Build React app
FROM node:18 AS build
WORKDIR /app

# Copy only package files first (for caching)
COPY my-react-app/package*.json ./
RUN npm install

# Copy the rest of the app
COPY my-react-app/. .
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]