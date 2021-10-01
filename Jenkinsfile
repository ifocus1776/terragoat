pipeline {
    agent {
        docker {
            image 'kennethreitz/pipenv:latest'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('test') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], userRemoteConfigs: [[url: 'https://github.com/ifocus1776/terragoat.git']]])
                script {
                    sh "pipenv install"
                    sh "pipenv run pip install bridgecrew"
                    sh "pipenv run bridgecrew --directory .  --bc-api-key c2187b1a-02cf-5765-a714-7a67ecc3566f --repo-id ifocus1776/terragoat"
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}
