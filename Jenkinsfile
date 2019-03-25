pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    environment {
        YC_ACCOUNT_KEY_FILE = "/opt/yandex-packer/packer-key.json"
        YC_FOLDER_ID = "b1g9mev5371kagqd9muk"
        YC_SUBNET_ID = "e2l67sljle77f206f9gs"
    }
    stages {
        stage('Build') {
            steps {
                sh label: '', script: '/opt/yandex-packer/packer -color=false build ./packer/base.json'
            }
        }
        stage('Test') {
            steps {
                parallel(
                    a: {
                        sh label: '', script: '/opt/yandex-packer/packer -color=false build ./packer/nginx.json'
                    },
                    b: {
                        sh label: '', script: '/opt/yandex-packer/packer -color=false build ./packer/django.json' 
                    }
                )
            }
        }
    }
}

