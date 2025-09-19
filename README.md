# Laravel Docker Examples Project

### Atention
Это лабораторная работа, так что не советую использовать этот репозиторий, если вы не мой препод)

This is not a real project, just my education lab, dont use it in real life

Основанно на ```https://github.com/rw4lll/laravel-docker-examples```

### Зависимости

- Docker
- docker-compose

### Clone the Repository

```bash
git clone https://github.com/Nikolay-Yakunin/laravel-docker-examples-main.git
cd laravel-docker-examples-main
```

### Предварительные действия

1. Скопируйте окружение:

```bash
cp .env.example .env
```

Hint: adjust the `UID` and `GID` variables in the `.env` file to match your user ID and group ID. 

Чтобы посмотреть свой **UID** ```$UID```

Чтобы посмотреть свой **GID** ```id -g your_user_name```

2. Запуск в дев режиме:

```bash
docker compose -f compose.dev.yaml up -d
```

3. Установка зависимостей:

```bash
docker compose -f compose.dev.yaml exec workspace bash
composer install
npm install
npm run dev
```

4. Запуск миграции:

```bash
docker compose -f compose.dev.yaml exec workspace php artisan migrate
```

5. Результат в браузере:

Откройте браузер, и перейдите на [http://localhost:8080](http://localhost:8080).

Если вы хотите изменить порт на 80, то в некоторых браузерах, из за политики безопасности, у вас будет автозамена http на https, и соответсвенное, вы ничего не увидите.

## Usage

Here are some common commands and tips for using the development environment:

### Accessing the Workspace Container

The workspace sidecar container includes Composer, Node.js, NPM, and other tools necessary for Laravel development (e.g. assets building).

```bash
docker compose -f compose.dev.yaml exec workspace bash
```

### Run Artisan Commands:

```bash
docker compose -f compose.dev.yaml exec workspace php artisan migrate
```

### Rebuild Containers:

```bash
docker compose -f compose.dev.yaml up -d --build
```

### Stop Containers:

```bash
docker compose -f compose.dev.yaml down
```

### View Logs:

```bash
docker compose -f compose.dev.yaml logs -f
```

For specific services, you can use:

```bash
docker compose -f compose.dev.yaml logs -f web
```

## Production Environment

The production environment is designed with security and efficiency in mind:

- **Optimized Docker Images**: Uses multi-stage builds to minimize the final image size, reducing the attack surface.
- **Environment Variables Management**: Sensitive data such as passwords and API keys are managed carefully to prevent exposure.
- **User Permissions**: Containers run under non-root users where possible to follow the principle of least privilege.
- **Health Checks**: Implemented to monitor the status of services and ensure they are functioning correctly.
- **HTTPS Setup**: While not included in this example, it's recommended to configure SSL certificates and use HTTPS in a production environment.


### Deploying

The production image can be deployed to any Docker-compatible hosting environment, such as AWS ECS, Kubernetes, or a traditional VPS.

## Technical Details

- **PHP**: Version **8.4 FPM** is used for optimal performance in both development and production environments.
- **Node.js**: Version **22.x** is used in the development environment for building frontend assets with Vite.
- **PostgreSQL**: Version **16** is used as the database in the examples, but you can adjust the configuration to use MySQL if preferred.
- **Redis**: Used for caching and session management, integrated into both development and production environments.
- **Nginx**: Used as the web server to serve the Laravel application and handle HTTP requests.
- **Docker Compose**: Orchestrates the services, simplifying the process of starting and stopping the environment.
- **Health Checks**: Implemented in the Docker Compose configurations and Laravel application to ensure all services are operational.


## Contributing

В честь уважения, оригинальному репозиторию, который очень помог.

Contributions are welcome! Whether you find a bug, have an idea for improvement, or want to add a new feature, your input is valuable.

### How to Contribute

1. **Fork the Repository:**

   Click the "Fork" button at the top right of this page to create your own copy of the repository.

2. **Clone Your Fork:**

```bash
    git clone https://github.com/your-user-name/laravel-docker-examples.git
    cd laravel-docker-examples
```

3. Create a Branch:

```bash
    git checkout -b your-feature-branch
```

4. Make Your Changes.

    Implement your changes or additions.

5. Commit Your Changes:

```bash
git commit -m "Description of changes"
```

6. Push to Your Fork:

```bash
    git push origin feature-branch
```

7. Submit a Pull Request:
    - Go to the original repository.
    - Click on "Pull Requests" and then "New Pull Request."
    - Select your fork and branch, and submit your pull request.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
