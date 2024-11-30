# Use a lightweight MySQL image
FROM mariadb:11.4.4-noble

# Set the default authentication plugin
ENV MYSQL_ROOT_PASSWORD=your_root_password
ENV MYSQL_USER=your_db_user
ENV MYSQL_PASSWORD=your_db_password

# Expose the MySQL port
EXPOSE 3306

# Set the command to start MySQL with the specified authentication plugin
CMD ["--authentication-policy=mysql_native_password"]
