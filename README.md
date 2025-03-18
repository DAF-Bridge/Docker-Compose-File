# Docker-Compose-File
This is the compose file for deployment

## For first initial deployment
```
docker compose up --build -d
```

## If you want to down the compose file
```
docker compose down
```

If you have already setup Jenkins pipeline for CI/CD <br />
You can just add the "docker compose up -d" command in the pipeline and let the magic happen.
