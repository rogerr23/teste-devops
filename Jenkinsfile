pipeline {
    agent any

    stages {
        stage('Acessibilidade') {
            steps {
                withCredentials([sshUserPrivateKey(
                    credentialsId: 'jenkins',
                    keyFileVariable: 'keyfile',
                    usernameVariable: 'username'
                )]) {
                    script {
                        sh '''
                            if ! command -v pa11y &> /dev/null; then
                                npm install -g pa11y
                            fi

                            mkdir -p reports/acessibilidade

                            pa11y http://teste-devops \
                                --standard WCAG2AA \
                                --reporter html \
                                --timeout 60000 \
                                --wait 2000 \
                                > reports/acessibilidade/relatorio.html \
                                || echo "Aviso: falha ao gerar relatório HTML"

                            echo "----- Resultado dos testes de acessibilidade -----"
                            pa11y http://teste-devops \
                                --standard WCAG2AA \
                                --reporter cli \
                                --timeout 60000 \
                                --wait 2000 \
                                || echo "Foram encontrados problemas de acessibilidade. Verifique o relatório."
                        '''
                    }
                }
            }
        }
    }

    post {
        always {
            publishHTML(target: [
                allowMissing         : false,
                alwaysLinkToLastBuild: true,
                keepAll              : true,
                reportDir            : 'reports/acessibilidade',
                reportFiles          : 'relatorio.html',
                reportName           : 'Relatório de Acessibilidade'
            ])
        }
        failure {
            echo 'Stage de acessibilidade falhou. Verifique o relatório para detalhes.'
        }
    }
}