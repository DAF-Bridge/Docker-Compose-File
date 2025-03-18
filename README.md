# __Docker-Compose-File__
This is the compose file for deployment

## For first initial deployment
You have to put the environment variables in the '<*>' format in order to make this compose file runnable.
```
docker compose up --build -d
```

## If you want to down the compose file
```
docker compose down
```

## Jenkins
If you have already setup Jenkins pipeline for CI/CD. <br />
You can just add the "docker compose up -d" command in the pipeline stage and let the magic happen. <br />

**!!!Cautions!!!**: <br />
You have to be careful when using docker compose up & docker compose down with jenkins in this file <br />
for further improvement I suggest you should separate this docker compose file into mulitple files so that you can <br />
prioritize the order of compose file & can specify what compose file that can be compose up & down without crashing the system.
