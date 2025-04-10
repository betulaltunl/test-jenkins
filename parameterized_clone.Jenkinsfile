pipelineJob('Choice-Parameterized-Git-Clone') {
    description('Kullanıcıya sunulan listeden branch seçtirerek repo klonlar.')

    parameters {
        choiceParam(
            'BRANCH_TO_CLONE',
            ['main', 'master', 'develop', 'release/v1.0'],
            'Klonlanacak Git Branch Adını Seçin'
        )
    }

    definition {
        cps {
            script("""
                pipeline {
                    agent any
                    parameters {
                        choice(name: 'BRANCH_TO_CLONE', choices: ['main', 'master', 'develop', 'release/v1.0'], description: 'Klonlanacak Git Branch Adını Seçin')
                    }
                    stages {
                        stage('Clean Workspace') {
                            steps {
                                cleanWs()
                            }
                        }
                        stage('Clone Repository') {
                            steps {
                                echo "Repo klonlanıyor: https://github.com/betulaltunl/test-jenkins.git"
                                echo "Seçilen Branch: \${params.BRANCH_TO_CLONE}"

                                checkout([
                                    \$class: 'GitSCM',
                                    branches: [[name: "\${params.BRANCH_TO_CLONE}"]],
                                    userRemoteConfigs: [[url: 'https://github.com/betulaltunl/test-jenkins.git']],
                                    extensions: [[\$class: 'RelativeTargetDirectory', relativeTargetDir: 'source-code']]
                                ])

                                echo "Klonlama tamamlandı."
                            }
                        }
                    }
                }
            """.stripIndent())
            sandbox(true)
        }
    }
}
