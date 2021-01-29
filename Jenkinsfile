pipeline {    

    agent any    
    
    environment {
        DTR_FQDN_PORT='ec2-18-197-143-139.eu-central-1.compute.amazonaws.com:4443'
    }

    stages {
        stage('Build') {
            environment {
                DTR_ACCESS_KEY = credentials('jenkins-dtr-access-token')
        MAJORMINOR = '0.0'
            }
            steps {
            sh 'docker --context=buildserver image build -t \
                ec2-18-197-143-139.eu-central-1.compute.amazonaws.com:4443/engineering/api-build:rc-${MAJORMINOR}.${BUILD_ID} \
                api'
            sh 'docker --context=buildserver login -u jenkins -p ${DTR_ACCESS_KEY} ec2-18-197-143-139.eu-central-1.compute.amazonaws.com:4443'
            sh 'docker --context=buildserver image push \
                ec2-18-197-143-139.eu-central-1.compute.amazonaws.com:4443/engineering/api-build:rc-${MAJORMINOR}.${BUILD_ID}'
            }
        }
    }
    
    post {
        always{
            sh 'rm -rf ${WORKSPACE}/*'
        }
    }
}
