# docker-wordpress

## 📝 Why?
You can use docker if you want to share your WordPress project with your client. It will help you to share your project with clients in an easy way. You already know if you use docker then your client does not need to set up a WordPress environment simply if he has docker that's great.  I can do this fast. You can use any one of them.

## 🛠 Code
```bash
# YAML is a human-readable data-serialization language. It is commonly used for configuration files and in applications where data is being stored or transmitted. 

version: '3.1'  # Compose file versions

services:
  # mysql Database
  db:
    image: mysql:5.7
    volumes: 
      - db_data:/var/lib/mysql
    restart: always #Database will restart with container
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: WordPress
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    networks:
      - wpNetwork #it can be any name
  # phpmyadmin
  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin # Please use image: phpmyadmin instead of image: phpmyadmin/phpmyadmin for better security
    restart: always 
    ports:
      - "8080:80" # 80 HTTP port
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: password
    networks:
      - wpNetwork  # should be same as Database

  #WordPress
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    restart: always
    volumes: ["./:/var/www/html"]
    environment:
      WORDPRESS_DB_HOST: db:3306 # mysql Default Port
      WORDPRESS_DB_USER: user # Same as Database
      WORDPRESS_DB_PASSWORD: password # Same as Database
      WORDPRESS_DB_NAME: WordPress
    networks:
      - wpNetwork   # should be same as Database
networks:
  wpNetwork:
volumes:
  db_data: 
```

## 💻 Tarminal code
```bash
  docker-compose up -d
```



## 🧑‍💻 Contributors
- [@Ali Hossain](https://github.com/shovoalways/)


## 🥰 Follow me
- [@Github](https://github.com/shovoalways/) 
- [@Facebook](https://facebook.com/shovoalways/) 
- [@Twitter](https://twitter.com/shovoalways/) 
- [@Instagram](https://instagram.com/shovoalways/) 
