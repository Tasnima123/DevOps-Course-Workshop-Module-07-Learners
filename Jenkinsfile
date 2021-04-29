pipeline {
    agent none {}
    environment {
        DOTNET_CLI_HOME = "/tmp/dotnet_cli_home"
    }
    stages {
        stage('Build npm') {
            agent {
                docker { 
                    image 'node:14-alpine' 
                    label 'docker-node'
                    }
            }
            steps {
                dir("DotnetTemplate.Web") {
                    sh "npm run build"
                }
            }
        }
        stage('build dotnet'){
            agent {
                docker { 
                    image '5.0-alpine' 
                    label 'docker-dotnet'
                    }
            }
        }
        stage('Test') {
            steps {
                sh "dotnet test"
                dir("DotnetTemplate.Web") {
                    sh "npm t"
                    sh "npm run lint"
                }
            }
        }
    }
}