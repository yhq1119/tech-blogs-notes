MySQL - PHP Error FIX

# 1. error: mysqli_connect(): The server requested authentication method unknown to the client [caching_sha2_password] in...

Simple Solution: 
After enter mysql shell, use the command below:
- If you had already created the user and the password:

`mysql
ALTER USER 'mysqlUsername'@'localhost' IDENTIFIED WITH mysql_native_password BY 'mysqlUsernamePassword';
`
- If not:

`mysql
CREATE USER 'jeffrey'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
`
