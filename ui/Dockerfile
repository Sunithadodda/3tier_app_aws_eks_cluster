# Use the official Nginx image to serve the frontend
FROM nginx:alpine

# Copy the frontend files into the Nginx directory
COPY . /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80

# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]