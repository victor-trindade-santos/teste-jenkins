stage('Detect Changes') {
    steps {
        script {
            // Atualiza status do Git
            bat 'git fetch origin main'
            def status = bat(script: 'git status --porcelain', returnStdout: true).trim()

            if (status) {
                echo "Alterações detectadas:\\n${status}"
                // Faz commit apenas se houver modificações válidas
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
