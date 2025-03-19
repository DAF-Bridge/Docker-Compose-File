# __Docker-Compose-File__
This is the compose file for deployment

## For first initial deployment
You have to replace the environment variables in the '<*>' format with your environment variable in order to make this compose file runnable. <br />
After the first compose up finised, you have to run the connector-cdc curl commmand to make connection between the PostgreSQL & Debezium which you <br />
can find the curl command in the Kafka-Consumer-CDC repository after that restart the consumer containers again to fully deploy the project. 
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

### Example Jenkins Script:
```groovy
pipeline {
    agent { label 'JenkinsSlave' }
    
    environment {
        GITHUB_USER = credentials('github-username')
        GITHUB_TOKEN = credentials('github-token')
        IMAGE_NAME = 'ghcr.io/daf-bridge/talent-atmos-backend:latest
        COMPOSE_DIR = '/home/raiwin/daf-bridge' // Change this to your actual compose file directory
    }
    
    stages {
        stage('Login to GitHub Container Registry') {
            steps {
                script {
                    sh "echo \"$GITHUB_TOKEN\" | docker login ghcr.io -u $GITHUB_USER --password-stdin"
                }
            }
        }
        
        stage('Pull Image') {
            steps {
                script {
                    sh "docker pull $IMAGE_NAME"
                }
            }
        }
        
        stage('Verify Image') {
            steps {
                script {
                    sh "docker images | grep \"talent-atmos-backend\""
                }
            }
        }
        
        stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh "cd $COMPOSE_DIR && docker compose up -d"
                }
            }
        }
    }
    
    post {
        always {
            sh "docker logout ghcr.io"
        }
    }
}
```

**!!!Cautions!!!**: <br />
You have to be careful when using docker compose up & docker compose down with jenkins in this file <br />
for further improvement I suggest you should separate this docker compose file into mulitple files so that you can <br />
prioritize the order of compose file & can specify what compose file that can be compose up & down without crashing the system.
