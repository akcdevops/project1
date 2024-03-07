pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('git checkout') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/akcdevops/project1.git'
                
            }
        }
        stage('Build'){
            steps{
               sh 'mvn clean package'
            }
        }
        stage('Upload'){
            steps{
               script{
                 withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'awscred', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                        // Copy .war file to S3 bucket
                        sh 'aws s3 cp target/*.war s3://akcdevops/project-1/'
                    }
               } 
            }

        }
        
    }
}
