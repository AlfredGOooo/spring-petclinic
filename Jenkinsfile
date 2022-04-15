pipeline {
    agent any
    stages{
        tools {
            maven "maven-3"
        }
        
        stage('Local Download') {
            steps {
                git url: 'https://github.com/AlfredGOooo/spring-petclinic.git', branch: 'main',
                 credentialsId: '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'
            }
        }
        
        stage('Clean Up') {
            steps {
                withMaven {
                    sh './mvnw clean'
                }
            }
        }

        stage('Compile Project') {
            steps {
                withMaven {
                    sh './mvnw install'
                }
            }
        }
        
        stage('Ansible Step') {
            steps {
                sh 'ansible-playbook /vagrant/deploy-jar.yml'
            }
        }
    }
    post{
        success{
            echo "Build Success"
        }
        failure{
            echo "Build Failed"
        }
    }
}
