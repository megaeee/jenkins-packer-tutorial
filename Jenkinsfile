environment {
    YC_ACCOUNT_KEY_FILE = "~/.packer/packer-key.json"
    YC_FOLDER_ID = "b1g9mev5371kagqd9muk"
    YC_SUBNET_ID = "e2l67sljle77f206f9gs"
}

pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
               withEnv(['YC_ACCOUNT_KEY_FILE=~/.packer/packer-key.json']) {
                  sh label: '', script: '/opt/packer/packer build ./packer/base.json'
               }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }
}

