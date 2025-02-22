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
                bat 'kubectl validate k8s-manifestfiles.yaml'
            }
       }

        stage("Verify deployment"){
           steps{
             bat 'kubectl get pods'
           }
        }

    }
}