pipeline {
    agent any
    stages{
        stage('clean up') {
            steps {
                withMaven {
                    sh './mvnw clean'
                }
            }
        }

        stage('compile project') {
            steps {
                withMaven {
                    sh './mvnw install'
                }
            }
        }

        stage('SonarQube analyize') {
            steps {
                withSonarQubeEnv('YuxinsSonar') {
                    withMaven {
                        sh './mvnw sonar:sonar'
                    }
                }
            }
        }
    }
    post{
        success{
            archiveArtifacts 'target/*.jar'
        }
        failure{
            echo '=========================='
            echo 'Build fail!!!!!!!!!!!!!!!!'
            echo '=========================='
        }
    }
}
