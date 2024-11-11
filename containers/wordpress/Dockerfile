# Use a lightweight WordPress image
FROM wordpress:6.6-php8.2-fpm-alpine

# Copy the WordPress configuration and content
# COPY wordpress/ /var/www/html/

# Set environment variables
ENV WORDPRESS_DB_HOST=db:3306
ENV WORDPRESS_DB_USER=your_db_user
ENV WORDPRESS_DB_PASSWORD=your_db_password
ENV WORDPRESS_DB_NAME=wordpress

# Expose the WordPress port (if needed, adjust based on your setup)
EXPOSE 9000

# Set the command to start the WordPress application
CMD ["php-fpm"]
