pipeline {
    agent any

    stages {
        stage('Check SonarScanner Installation') {
            steps {
                script {
                    def scannerHome = tool 'MySonarScanner'
                    echo "Scanner: ${scannerHome}"

                    bat "dir \"${scannerHome}\\bin\\sonar-scanner.bat\""
                    bat "\"${scannerHome}\\bin\\sonar-scanner.bat\" -v"
                }
            }
        }

        stage('Checkout from GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/sayfboukh123/carProjet'
            }
        }

        stage('Analyse SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'MySonarScanner'

                    withSonarQubeEnv('projet') {
                        withCredentials([string(credentialsId: 'sonarqube', variable: 'TOKEN')]) {
                            bat "\"${scannerHome}\\bin\\sonar-scanner.bat\" " +
                                "-Dsonar.projectKey=node-projetcid " +
                                "-Dsonar.sources=. " +
                                "-Dsonar.login=%TOKEN% " +
                                "-Dsonar.projectVersion=1.0.0 " +
                                "-Dsonar.sourceEncoding=UTF-8"
                        }
                    }
                }
            }
        }
    }
}
