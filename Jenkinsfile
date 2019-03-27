pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    environment {
        YC_ACCOUNT_KEY_FILE = credentials('YC_ACCOUNT_KEY_FILE')
        YC_FOLDER_ID = credentials('YC_FOLDER_ID')
        YC_SUBNET_ID = credentials('YC_SUBNET_ID')

        PACKER_SH = '/opt/yandex-packer/packer build -color=false'
    }
    stages {
        stage('Build') {
            steps {
                sh label: '', script: "${env.PACKER_SH} ./packer/base.json"
            }
        }
        stage('Test') {
            steps {
                parallel(
                    a: {
                        sh label: '', script: '${env.PACKER_SH} ./packer/nginx.json'
                    },
                    b: {
                        sh label: '', script: '${env.PACKER_SH} ./packer/django.json' 
                    }
                )
            }
        }
    }
}

