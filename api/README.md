# Dify Backend API

## Usage

1. Start the docker-compose stack

   The backend require some middleware, including PostgreSQL, Redis, and Weaviate, which can be started together using `docker-compose`.
   修改目录所有者为501账户后，在启动容器，否则会出现权限问题导致容器无法启动。
   ```bash
   export UID=$(id -u)
   export GID=$(id -g)

   cd ../docker
   sudo chown -R 501:501 ./volumes

   docker-compose -f docker-compose.middleware.yaml up -d
   cd ../api
   ```
2. Copy `.env.example` to `.env`
3. Generate a `SECRET_KEY` in the `.env` file.

   ```bash
   openssl rand -base64 42
   ```
4. Install dependencies
   ```bash
   pip install -r requirements.txt
   ```
5. Run migrate

   Before the first launch, migrate the database to the latest version.

   ```bash
   flask db upgrade
   ```
6. Start backend:
   ```bash
   flask run --host 0.0.0.0 --port=5001 --debug
   ```
7. Setup your application by visiting http://localhost:5001/console/api/setup or other apis...
