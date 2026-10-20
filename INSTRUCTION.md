# Instructions for Running the Todo App with Docker Compose

## Prerequisites & Getting the Code

- **Docker Engine** installed on your system.
- **Git** installed on your system.
- **Note for Linux users:** If your user is not added to the `docker` group, you will need to prepend `sudo` to all Docker commands.

First, clone your fork of the repository to your local machine, switch to the correct branch, and navigate into the project directory:

```bash
git clone https://github.com/dimamikolaichuk13-jpg/devops_todolist_docker_core_task_3_docker_compose.git
cd devops_todolist_docker_core_task_3_docker_compose
git checkout DockerCompose
```

## Running the Application

Docker Compose automatically handles network connections, health checks, and build order for both the MySQL database and the Django application.

1. Build and start the containers in the foreground (useful for viewing logs directly):

```bash
docker compose up --build
```

2. Build and start the containers in the background (detached mode):

```bash
docker compose up -d --build
```

**Note on First Run:** MySQL may take up to a minute to initialize its database files on the very first start. Thanks to the health check configuration, the Django app will wait automatically and start correctly once the database is fully ready.

## Accessing the Application via a Browser

Once the services are running and healthy, open your web browser and navigate to:

http://localhost:8080

**Expected Output:** You should see the interactive Django Todo application dashboard, where you can create, view, and manage your tasks.

## Checking Status and Logs

1. Check the running containers and their status:

```bash
docker compose ps
```

2. View aggregated logs from all services:

```bash
docker compose logs
```

## Verifying Data Persistence

To ensure that the MySQL volume (`db-data`) successfully persists your data:

1. Open the application in your browser at:

http://localhost:8080

2. Add a new todo task.

3. Stop the containers using `docker compose down`. Make sure **not** to use `-v`, as `-v` deletes volumes.

```bash
docker compose down
```

4. Restart the application:

```bash
docker compose up -d
```

5. Refresh the application at http://localhost:8080.

Your previously added task should still be there, confirming that the database data is persisted in the volume.

## Stopping the Application

1. Stop and remove containers and networks while preserving database data in the volume:

```bash
docker compose down
```

2. Stop and remove containers, networks, **and volumes**.

**Warning:** This permanently deletes all database data.

```bash
docker compose down -v
```

## Notes and Troubleshooting

- **Port Conflicts:** Ensure that port `8080` is free on your host machine. If you have any old running containers from previous tasks, make sure to stop and remove them before running `docker compose up`.

```bash
docker stop <container_name>
docker rm <container_name>
```
