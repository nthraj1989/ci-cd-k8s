pipeline{

    agent any
    tools{
        maven "maven"
    }

    stages{

        stage("SCM checkout"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/nthraj1989/ci-cd-k8s.git']])
            }
        }

        stage("Build Process"){
            steps{
                script{
                    bat 'mvn clean install'
                }
            }
        }

        stage("Build Image") {
            steps{
                script{
                    bat 'docker build -t niitrajnish/spring-ci-cd:1.0 .'
                }
            }
        }

       stage("Deploy to k8s"){
        steps{
           script{
            bat 'kubectl apply -f namespace.yaml --validate=false'
            bat 'kubectl apply -f deployment.yaml --validate=false'
            bat 'kubectl apply -f service.yaml --validate=false'
           }
         }
       }

    }
}