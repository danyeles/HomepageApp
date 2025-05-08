pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'ghcr.io/gethomepage/homepage:latest'
        CONTAINER_NAME = 'homepage'
        PUID = '1000'
        PGID = '1000'
        TZ = 'America/Monterrey'
        WEBUI_PORTS = '3000/tcp,3000/udp'
        CONFIG_PATH = '/home/docker/homepage/config'
    }

    stages {
        stage('Deploy Homepage Docker Image') {
            steps {
                script {
                    sh """                      
                    docker run -d \
                        --restart always \
                        --name ${CONTAINER_NAME} \
                        -e HOMEPAGE_ALLOWED_HOSTS=gethomepage.dev,192.168.100.60,192.168.100.60:3000 \
                        -p 3000:3000 \
                        -e PUID=${PUID} \
                        -e PGID=${PGID} \
                        -e TZ=${TZ} \
                        -v /var/run/docker.sock:/var/run/docker.sock:ro \
                        -v ${CONFIG_PATH}:/config \
                        ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
