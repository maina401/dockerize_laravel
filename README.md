# Dockerizing Laravel App

This project demonstrates the Dockerization of a Laravel application, making it easy to package and deploy the application with its dependencies. Docker allows for consistent and reproducible deployments across different environments, making it ideal for managing Laravel applications.

## Prerequisites

Before you begin, ensure that you have the following prerequisites installed on your system:

- Docker: [Install Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [Install Docker Compose](https://docs.docker.com/compose/install/)

## Project Structure

The project consists of the following files and directories:

- `docker-compose.yml`: The main configuration file that defines the services and their dependencies.
- `docker/app.dockerfile`: Dockerfile for building the application service.
- `docker/nginx/db_balancer.conf`: Nginx configuration file for the database balancer service.
- `docker/nginx/nginx.conf`: Nginx configuration file for the web server service.
- `docker/nginx/web_balancer.conf`: Nginx configuration file for the web balancer service.

## Services

This project defines the following services:

- **app**: The Laravel application service. It builds the application image using the `docker/app.dockerfile` and mounts the application code inside the container.
- **db_balancer**: Nginx service that acts as a load balancer for the database service.
- **web**: Nginx service that serves the Laravel application. It also acts as a load balancer for multiple replicas of the application service.
- **web_balancer**: Nginx service that acts as a load balancer for the web service. It is exposed on port 9091 of the host machine.
- **database**: MySQL database service. It uses the official `mysql:8.0` Docker image and persists data in the `dbdata` volume.
- **pma**: phpMyAdmin service for managing the database. It depends on the `database` service and is exposed on port 9988 of the host machine.

## Configuration

You can customize the configuration of the services using environment variables defined in the `.env` file or directly in your shell environment. The following environment variables are used:

- **DB_DATABASE**: The name of the MySQL database.
- **DB_PASSWORD**: The password for the MySQL root user and the application database user.
- **DB_USERNAME**: The username for the application database user.
- **DB_PORT**: The port on which the MySQL service is exposed.

## Usage

Follow these steps to run the Laravel application using Docker:

1. Clone this repository: `git clone <repository_url>`
2. Navigate to the project directory: `cd <project_directory>`
3. Create a `.env` file and set the required environment variables (refer to the Configuration section).
4. Build and start the services: `docker-compose up --build -d`
5. Access the Laravel application in your web browser: `http://localhost`
6. Access phpMyAdmin to manage the database: `http://localhost:9988`

## Scaling the Application

By default, the `app` and `web` services are configured to run with five replicas. You can scale the application horizontally by increasing or decreasing the number of replicas. Use the following command:

```bash
docker-compose up --scale app=<num_replicas> --scale web=<num_replicas>
```

Replace `<num_replicas>` with the desired number of replicas.

## Maintenance and Troubleshooting

- To stop the services, run: `docker-compose down`
- To view logs of a specific service, run: `docker-compose logs <service_name>`
- If you encounter any issues, make sure that your system meets the prerequisites and check the logs for error messages.

## Conclusion

Dockerizing a Laravel application simplifies the deployment process by encapsulating the application and its dependencies in containers. With this project, you can easily package and deploy your Laravel application using Docker, ensuring consistency and portability across different environments.