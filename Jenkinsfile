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

        stage('Copy Archive') {
             steps {
                 script {
                    step ([$class: 'CopyArtifact',
                        projectName: 'spring-petclinic',
                        filter: "target/*.jar",
                        target: '/vagrant']);
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
