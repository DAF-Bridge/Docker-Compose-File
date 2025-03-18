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

## Jenkins
If you have already setup Jenkins pipeline for CI/CD <br />
You can just add the "docker compose up -d" command in the pipeline and let the magic happen. <br />
!!!Cautions: you have to be careful when using docker compose up & docker compose down with jenkins in this file <br />
for further improvement I suggest you should separate this docker compose file into mulitple files so that you can <br />
prioritize the order of compose file & can specify what compose file that can be compose up & down without crashing the system
