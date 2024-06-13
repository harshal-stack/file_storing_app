#FROM node:17-alpine

#WORKDIR /app

#COPY . .

#RUN npm install -g @angular/cli

#EXPOSE 4200

#CMD  ["node", "--openssl-legacy-provider", "/usr/local/bin/ng", "serve", "--host", "0.0.0.0"]


# Stage 1: Build Stage
FROM node:20-alpine AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Clean npm cache
#RUN npm cache clean --force

# Start an interactive shell for debugging
#RUN /bin/sh

# Install dependencies with retry and verbose logging
#RUN npm install --verbose || npm install --verbose

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Copy the rest of the application code
COPY . .

# Build the Angular application

# Stage 2: Serve Stage
FROM nginx:alpine

# Copy the built Angular application from the build stage
COPY --from=build /app/dist/FileStorage-SPA /usr/share/nginx/html

# Copy custom Nginx configuration (optional)
# Ensure nginx.conf exists in your project directory if using this line
# COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]

