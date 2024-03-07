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
        
    }
}
