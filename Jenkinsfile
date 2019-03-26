pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    environment {
        YC_ACCOUNT_KEY_FILE = credentials('YC_ACCOUNT_KEY_FILE')
        YC_FOLDER_ID = credentials('YC_FOLDER_ID')
        YC_SUBNET_ID = credentials('YC_SUBNET_ID')
    }
    stages {
        stage('Build') {
            steps {
                sh label: '', script: '/opt/yandex-packer/packer build -color=false ./packer/base.json'
            }
        }
        stage('Test') {
            steps {
                parallel(
                    a: {
                        sh label: '', script: '/opt/yandex-packer/packer build -color=false ./packer/nginx.json'
                    },
                    b: {
                        sh label: '', script: '/opt/yandex-packer/packer build -color=false ./packer/django.json' 
                    }
                )
            }
        }
    }
}

