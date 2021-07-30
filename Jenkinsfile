pipeline {    

    agent any    
    
    environment {
        MSR_FQDN_PORT='fmhdsagwnswjmybyp-2qtac556tyjufmasg.labs.strigo.io:4443'
    }

    stages {
        stage('Build') {
            environment {
                MSR_ACCESS_KEY = credentials('03818956-e0dd-40d9-8010-10c60f4db602')
        MAJORMINOR = '0.0'
            }
            steps {
            sh 'docker --context=buildserver image build -t \
                ${MSR_FQDN_PORT}/engineering/api-build:rc-${MAJORMINOR}.${BUILD_ID} \
                api'
            sh 'docker --context=buildserver login -u jenkins -p ${MSR_ACCESS_KEY} ${MSR_FQDN_PORT}'
            sh 'docker --context=buildserver image push \
                ${MSR_FQDN_PORT}/engineering/api-build:rc-${MAJORMINOR}.${BUILD_ID}'
            }
        }
    }
    
    post {
        always{
            sh 'rm -rf ${WORKSPACE}/*'
        }
    }
}
