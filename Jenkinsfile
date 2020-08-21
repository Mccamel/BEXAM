#!groovy

pipeline {
    agent any
    environment {
        registryCredentialSet = 'mccamel_id'
        imageName = 'mccamel/bexam'
    }
    stages {
        stage('build Static') {
            steps {
                sh "sed -i \'s/#BUILD_NO#/${env.BUILD_NUMBER}/g\' index.html "
                echo 'index.html updated'
            }
        }
        stage('Build Image') {
            steps {
                    script {
                    app = docker.build('mccamel/bexam')
                    }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'mccamel_id') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push('latest')
                    }
                }
            }
        }
                stage('Deploy Image') {
            steps {
                script {
                   //installed kubectl on the jenkins docker image - after hiting a BUG with  https://issues.jenkins-ci.org/browse/JENKINS-63224
                   sh '/var/jenkins_home/bin/kubectl apply -f  kubernetes_deployments/nginx_deployment.yaml'
                   sh '/var/jenkins_home/bin/kubectl rollout restart deployment/nginx-deployment'
                }
            }
                }
    }
    post {
        always {
            echo 'I will always say Hello again!'
            emailext attachLog: true, body: '$DEFAULT_CONTENT',
            recipientProviders: [
                culprits()
            ],
            replyTo: '$DEFAULT_REPLYTO',
            subject: '$DEFAULT_SUBJECT'
        }
    }
}
