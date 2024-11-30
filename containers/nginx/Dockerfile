# Use a lightweight Nginx image
FROM nginx:1.27-alpine

# Copy Nginx configuration and custom HTML files
COPY config/ /etc/nginx/
COPY html/* /var/www/html/

# Expose the Nginx port
EXPOSE 80

# Set the command to start Nginx
CMD ["nginx", "-g", "daemon off;"]