pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }
   tools {

        maven 'MAVEN3'

    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build & Test with JaCoCo') {
            steps {
                script {
                    // Run Maven build and generate JaCoCo report
                    bat 'mvn clean verify jacoco:report'
                }
            }
        }
        
        stage('Publish JaCoCo Report') {
            steps {
                jacoco execPattern: '**/target/jacoco.exec', classPattern: '**/classes', sourcePattern: '**/src/main/java'
            }
        }
        
        // Add more stages if necessary, for example, for deploying
    }
    
    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }
    }
}
