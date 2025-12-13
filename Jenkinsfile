pipeline {
    agent {
        docker {
            image 'my-maven-git:latest'
            // Utiliser un volume Docker pour Maven plutôt que $HOME
            args '-v maven-repo:/root/.m2'
        }
    }
    options {
        // Supprime le workspace automatiquement avant chaque build
        skipDefaultCheckout(false)
    }
    stages {
        stage('Checkout') {
            steps {
                // Nettoyer le workspace proprement
                deleteDir()
                
                // Checkout avec les credentials Jenkins configurés
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                script {
                    echo "Current directory: ${pwd()}"
                    
                    // Navigate to the directory containing the Maven project 
                    dir('maven') { 
                    // Run Maven commands 
                        sh 'mvn clean test package'
                    }
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    // Exécuter le jar généré
                    dir('maven') { 
                    // Run Maven commands 
                        sh 'java -jar target/maven-0.0.1-SNAPSHOT.jar'
                    }
                }
            }
        }
    }
}
