pipeline {
    agent any

    tools {
        maven 'MAVEN3'
        jdk 'JDK17'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YacineChehata/timesheetproject.git'
            }
        }

        stage('Compile Stage') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('MVN SONARQUBE') {
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    bat """
                        mvn sonar:sonar ^
                        -Dsonar.projectKey=timesheet-devops ^
                        -Dsonar.host.url=http://192.168.33.10:9000 ^
                        -Dsonar.login=sonar-token
                    """
                }
            }
        }
    }
}
