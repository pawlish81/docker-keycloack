# Docker Compose Configuration for Keycloak with MariaDB

This Docker Compose file sets up Keycloak, an open-source Identity and Access Management solution, with a MariaDB database backend. The configuration includes volumes for persistent data storage and specifies environment variables for both MariaDB and Keycloak services.

#### Prerequisites

Docker and Docker Compose installed on your system.
Clone the repository:

```bash
git clone https://github.com/your-repository.git
```

```bash
cd your-repository
```
Create and start the containers:

```bash
docker-compose up -d
```

The -d flag runs the containers in the background.

Access Keycloak via your web browser:

```bash
http://localhost:8089
```

Use the following credentials to log in:

* Username: admin
* Password: Pa55w0rd


### Configuration Details
#### Volumes

* ##### mysql_data:
* Driver: local
* Purpose: Persistent volume for storing MariaDB data.

#### Services
MariaDB

* #### Image: mariadb

* #### Volumes: mysql_data:/var/lib/mysql: 

Mounts the persistent volume for MariaDB data.

#### Environment Variables:
* MYSQL_ROOT_PASSWORD: root
* MYSQL_DATABASE: keycloak
* MYSQL_USER: keycloak
* MYSQL_PASSWORD: password

* ##### Healthcheck:

Ensures that MariaDB is responsive using mysqladmin ping.

#### Keycloak
* Image: quay.io/keycloak/keycloak:legacy

#### Environment Variables:

* DB_VENDOR: mariadb
* DB_ADDR: mariadb
* DB_DATABASE: keycloak
* DB_USER: keycloak
* DB_PASSWORD: password
* KEYCLOAK_USER: admin
* KEYCLOAK_PASSWORD: Pa55w0rd
* JGROUPS_DISCOVERY_PROTOCOL: JDBC_PING

#### Ports:

* 8089:8080: 


This configuration assumes that you have a working Docker environment and Docker Compose installed.
Make sure no other services are using the ports specified in the configuration.

The provided Keycloak admin credentials are for initial login. Consider changing them for security reasons in a production environment.

Feel free to customize this Docker Compose file according to your specific requirements and security practices.