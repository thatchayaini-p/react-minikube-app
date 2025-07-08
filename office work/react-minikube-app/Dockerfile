# Use the official node image as a base image
FROM node:18-alpine as build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY ./package*.json ./

# Install dependencies inside the container
RUN npm install

# Copy the rest of the application files
COPY ./ ./

# Build the React app
RUN npm run build

# Use a smaller image (nginx) to serve the React app
FROM nginx:stable-alpine

# Copy the build folder from the build stage into the nginx html folder
COPY --from=build /app/build /usr/share/nginx/html

# Expose the port for nginx
EXPOSE 80

# Command to run the nginx server
CMD ["nginx", "-g", "daemon off;"]

