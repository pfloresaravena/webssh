pipeline {
    agent any
    environment{
        SONAR_SCANNER = tool 'SonarScanner'
    }
    stages {
        stage('SCM') {
            steps {
                checkout scm 
            }
        }

        stage('SAST') {
            steps {
                echo "Analizando código estático"
                withSonarQubeEnv('sonarqube-server'){
                    sh "${SONAR_SCANNER}/bin/sonar-scanner"
                }
                timeout(time: 3, unit: 'MINUTES'){
                waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
