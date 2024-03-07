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
        stage('Upload') {

        dir('/var/jenkins_home/workspace/'){

            pwd(); //Log current directory

            withAWS(region:'ap-south-1',credentials:'awscred') {

                 def identity=awsIdentity();//Log AWS credentials

                // Upload files from working directory 'dist' in your project workspace
                s3Upload(bucket:"akcdevops", workingDir:'project1/target', includePathPattern:'**/*.war');
            }

        };
    }
        
    }
}
