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
                copyArtifacts filter: 'target/*.jar', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: specific(env.BUILD_NUMBER), target: '/vagrant'
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
