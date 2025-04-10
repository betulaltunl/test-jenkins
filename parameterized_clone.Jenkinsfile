pipelineJob('Choice-Parameterized-Git-Clone') {
    description('Kullanıcıya sunulan listeden branch seçtirerek repo klonlar.')

    parameters {
        // === Choice Parametresi ===
        choiceParam(
            'BRANCH_TO_CLONE',                  // Parametre adı
            ['main', 'master', 'develop', 'release/v1.0'], // Seçenekler listesi 
            'Klonlanacak Git Branch Adını Seçin' 
        )
        
    }

    definition {
        cps {
            script("""
                pipeline {
                    agent any
                    parameters {
                         // Pipeline içinde de tanımla
                        choice(name: 'BRANCH_TO_CLONE', choices: ['main', 'master', 'develop', 'release/v1.0'], description: 'Klonlanacak Git Branch Adını Seçin')
                    }
                    stages {
                        stage('Clean Workspace') { /* ... */ }
                        stage('Clone Repository') {
                            steps {
                                echo "Repo klonlanıyor: https://github.com/betulaltunl/test-jenkins.git"
                                echo "Seçilen Branch: ${params.BRANCH_TO_CLONE}"

                                checkout([
                                    /$class: 'GitSCM',
                                    branches: [[name: params.BRANCH_TO_CLONE]],
                                    userRemoteConfigs: [[url: 'https://github.com/betulaltunl/test-jenkins.git']],
                                    extensions: [[ $class: 'RelativeTargetDirectory', relativeTargetDir: 'source-code' ]]
                                ])
    
                                echo "Klonlama tamamlandı."
                            }
                        }
                    }
                    post { /* ... */ }
                }
            """.stripIndent())
            sandbox(true)
        }
    }
}
