FROM node:latest as build
# Set the working directory
WORKDIR /app
# Add the source code to app
COPY ./your/app/root/folder ./
# Install all the dependencies
RUN npm install
# Generate the build of the application
RUN npm run build
# Stage 2: Serve app with nginx server
# Use official nginx image as the base image
FROM nginx:latest
COPY nginx.config /etc/nginx/conf.d/default.conf
# Copy the build output to replace the default nginx contents.
COPY --from=build /app/artifacts /usr/share/nginx/html
# Expose port 80
# EXPOSE 80
