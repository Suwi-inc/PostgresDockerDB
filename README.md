# PostgresDockerDB
# Deploying PostgreSQL using Docker on a Linux Server

This guide will walk you through the steps to deploy a PostgreSQL database on your Linux server using Docker. It includes pulling the image, creating a superuser role, and creating a database.

## Step 1: Install Docker

First, make sure Docker is installed on your Linux server. If it’s not installed, you can install it by running:

```bash
sudo apt-get update
sudo apt-get install -y docker.io 
```
## Step 2: Pull the PostgreSQL Docker Image
Next, pull the official PostgreSQL Docker image from Docker Hub:
```bash
sudo docker pull postgres
```

## Step 3: Run the PostgreSQL Container
Run the PostgreSQL container. Replace yourpassword with a secure password for the PostgreSQL superuser (default user postgres):

```bash
sudo docker run --name my-postgres-container -e POSTGRES_PASSWORD=yourpassword -d postgres
```
This command will start a PostgreSQL container named my-postgres-container with the superuser password set to yourpassword.
## Step 4: Access the PostgreSQL Container
To interact with the PostgreSQL instance, you need to access the container's shell:
```bash
sudo docker exec -it my-postgres-container bash
```
## Step 5: Access PostgreSQL Command Line Interface
Once inside the container, access the PostgreSQL command line interface (CLI):
```bash
psql -U postgres

```
## Step 6: Create a Superuser Role
To create a new superuser role, use the following command in the PostgreSQL CLI. Replace newuser and newpassword with your desired username and password:
```bash
CREATE ROLE newuser WITH LOGIN SUPERUSER PASSWORD 'newpassword';
```
## Step 7: Create a New Database
To create a new database, use the following command. Replace newdatabase with your desired database name:
```bash
CREATE DATABASE newdatabase;
```
## Step 8: Connect to Your New Database
You can now connect to your new database from within the container or from outside (e.g., using a PostgreSQL client). If connecting from outside, you need to ensure the container’s port is mapped to a port on your host machine. To do this, you can restart the container with port mapping:
```bash
sudo docker stop my-postgres-container
sudo docker rm my-postgres-container
sudo docker run --name my-postgres-container -e POSTGRES_PASSWORD=yourpassword -p 5432:5432 -d postgres
```
