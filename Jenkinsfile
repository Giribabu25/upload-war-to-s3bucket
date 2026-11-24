pipeline {
    agent any
    tools {
        maven "mymaven"
    }
    stages {
        stage('Code') {
            steps {
                git 'https://github.com/Giribabu25/dockerwebapp.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('Upload WAR to S3') {
            steps {
                step([
                    $class: 'S3BucketPublisher',
                    entries: [[
                        bucket: 'my-java-bob-bucket',
                        sourceFile: 'target/*.war',
                        selectedRegion: 'eu-north-1',
                        flatten: true
                    ]],
                    profileName: 'aws-s3'
                ])
            }
        }       
    }
}
