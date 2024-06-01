pipeline{
    agent any
    tools {
        maven 'Maven'
    }
    stages{
        stage("demo-test"){
            steps{
                git branch: 'main', url: 'https://github.com/coolgourav147/spring-boot-war-example'
                sh 'mvn test'
            }
        }
        stage("demo-build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("demo-depoly-test"){
            steps{
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
                deploy adapters: [tomcat9(credentialsId: '0ed4c001-da5e-42dc-ae1b-6b53bc1eb887', path: '', url: 'http://64.227.140.53:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
        stage("demo-deploy-prod"){
            steps{
                input message: 'should we continue?', ok: 'yes we should'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
                deploy adapters: [tomcat9(credentialsId: '0ed4c001-da5e-42dc-ae1b-6b53bc1eb887', path: '', url: 'http://139.59.45.143:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
