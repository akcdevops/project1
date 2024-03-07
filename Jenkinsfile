pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git  'https://github.com/akcdevops/project1.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Push .war to s3 Bucket'){
            steps{
                script{
                     withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) 
                    {
                         sh 'aws s3 cp target/*.war s3://akcdevops/project-1/'
                    }
                }
            }    
        }
    }
}
