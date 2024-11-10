# Use a lightweight WordPress image
FROM wordpress:6.6-php8.2-fpm-alpine

# Copy the WordPress configuration and content
# COPY wordpress/ /var/www/html/

# Set environment variables
ENV MYSQL_HOST=db:3306
ENV MYSQL_USER=your_db_user
ENV MYSQL_PASSWORD=your_db_password
ENV MYSQL_DATABASE=wordpress

# Expose the WordPress port (if needed, adjust based on your setup)
EXPOSE 80

# Set the command to start the WordPress application
CMD ["php-fpm"]
