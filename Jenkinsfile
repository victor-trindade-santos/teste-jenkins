pipeline {
    agent any

    triggers {
        cron('57 11 * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/victor-trindade-santos/teste-jenkins.git'
            }
        }

        stage('Detect Changes') {
            steps {
                script {
                    def status = bat(script: 'git status --porcelain', returnStdout: true).trim()

                    if (status) {
                        echo "Alterações detectadas:\\n${status}"
                        bat '''
                            git config user.name "jenkins-bot"
                            git config user.email "jenkins@example.com"
                            git add .
                            git diff --cached --quiet || (
                                git commit -m "Atualização automática pela pipeline Jenkins"
                                git push origin main
                            )
                        '''
                    } else {
                        echo "Nenhuma alteração detectada. Nada a fazer."
                    }
                }
            }
        }
    }
}
