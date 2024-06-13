pipeline {
    agent any

    environment {
        // SonarCloud variables
        SONAR_URL = 'https://sonarcloud.io/'
        SONAR_ORG = 'devsecops1-kb'
        SONAR_PROJECTKEY = 'devsecops1-kb'
        SONAR_LOGIN = '6388cfceaadf0f5725a5921b0d8dffb0f4648d53'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/devsecopsPipeline']],
                    userRemoteConfigs: [[url: 'https://github.com/kbrepository/simpleNodeApp.git']]
                ])
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'mvn install'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    script {
                        sh """
                            mvn sonar:sonar \
                            -Dsonar.host.url=${env.SONAR_URL} \
                            -Dsonar.organization=${env.SONAR_ORG} \
                            -Dsonar.projectKey=${env.SONAR_PROJECTKEY} \
                            -Dsonar.login=${env.SONAR_LOGIN}
                        """
                    }
                }
            }
        }
    }
    
    post {
        always {
            junit '**/target/surefire-reports/*.xml' // Publish test results
            cleanWs() // Clean workspace after build
        }
    }
}
