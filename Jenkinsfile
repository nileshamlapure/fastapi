pipeline {
    agent any


    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/nileshamlapure/fastapi.git'
            }
        }
        stage('Build') {
            steps {
                script{
                    sh "sudo docker build -t fastapi_app:latest ."
                }
            }
        }
        stage('Run Pylama') {
            when {
                branch 'master'
            }
            steps {
                script{
                    sh "pip install pylama[toml]"
                }
            }
        }
        stage('Approval-CodeOwner') {
            steps {
                script {
                    env.Release = input message: "Provide the owner approval", ok: "Done", parameters: [string(defaultValue: 'yes', name: 'Approval Status', trim: true)]
                    echo "Code Owner Approved"
                }
            }
        }
        stage('Deploy To UvicornDev') {
            steps {
                script{
                        sh 'sudo docker-compose up -d'
                }
            }
        }
        stage('Execute Tests') {
            steps {
                script{
                        sh "sudo docker-compose exec app pytest test/test.py"

                }
            }
        }
        stage('Push Image to Private Repo') {
            steps {
                script{
                    sh 'echo stage7'
                }
            }
        }
    }
}
