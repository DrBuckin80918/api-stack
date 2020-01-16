pipeline {    

    agent any    
    
    environment {
        DOCKER_TLS_VERIFY='1'                                                                                 
        COMPOSE_TLS_VERSION='TLSv1_2'                                                                        
        DOCKER_CERT_PATH='/home/jenkins/admincerts'                                                           
        DOCKER_HOST='tcp://ec2-18-189-143-135.us-east-2.compute.amazonaws.com:443'
        DTR_FQDN_PORT='ec2-18-189-143-135.us-east-2.compute.amazonaws.com:4443'
    }

    stages {
        stage('Build') {
            environment {
                DTR_ACCESS_KEY = credentials('jenkins-dtr-access-token')
            }
            steps {
                sh 'docker image build -t ${DTR_FQDN_PORT}/engineering/api-build:rc-1.0-build-${BUILD_ID} api'
                sh 'docker login -u jenkins -p ${DTR_ACCESS_KEY} ${DTR_FQDN_PORT}'
                sh 'docker image push ${DTR_FQDN_PORT}/engineering/api-build:rc-1.0-build-${BUILD_ID}'
            }
        }
    }
}
