# Step 1: Use Node.js as the base image
FROM node:18 AS build

# Step 2: Set working directory to /app
WORKDIR /app

# Step 3: Copy package.json and package-lock.json (for faster Docker builds)
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the application code
COPY . .

# Step 6: Build the production version of the app
RUN npm run build

# Step 7: Use a lightweight web server to serve the build
FROM nginx:alpine

# Step 8: Copy build output from previous step to Nginx's public folder
COPY --from=build /app/build /usr/share/nginx/html

# Step 9: Expose port 80 for the web server
EXPOSE 80

# Step 10: Start Nginx server
CMD ["nginx", "-g", "daemon off;"]