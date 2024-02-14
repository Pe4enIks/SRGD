# MLFlow

## Disclaimer
Don't push .env files to git, it's just an example without real credentials.

## Deploy Full

Compose Up.
```bash
docker compose build
docker compose up -d
```

Change MLFlow admin password.
```bash
curl --user "admin:password" \
    -X PATCH http://0.0.0.0:5000/api/2.0/mlflow/users/update-password \
    -H 'Content-Type: application/json' \
    -d '{"username":"admin","password":"new_password"}'
```

Create MLFlow user.
```bash
curl --user "admin:new_password" \
    -X POST http://0.0.0.0:5000/api/2.0/mlflow/users/create \
    -H 'Content-Type: application/json' \
    -d '{"username":"user","password":"password"}'
```

Check MLFlow user.

```bash
curl --user "admin:new_password" \
    -X GET http://0.0.0.0:5000/api/2.0/mlflow/users/get?username=user
```

Compose Down.
```bash
docker compose down --volumes
```

## Usage

Create MLFlow credentials (or use them as positional arguments in scripts)
```bash
mkdir -p ~/.mlflow
touch ~/.mlflow/credentials
```

MLFlow credentials example.
```text
[mlflow]
mlflow_tracking_username = user
mlflow_tracking_password = password
```