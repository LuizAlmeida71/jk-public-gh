pipeline {
    agent any

    stages {
        stage('Clonning Git Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/LuizAlmeida71/jk-public-gh.git'
            }
        }
        stage('Building Image') {
            steps {
                sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }
         stage('Deploy Application') {
            steps {
                sh '''
                    # Para e remove o contêiner antigo, se ele existir
                    docker stop webapp_ctr || true
                    docker rm webapp_ctr || true

                    # Executa o novo contêiner
                    docker run -d -p 8081:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
                '''
            }
        }
    }
}
