
pipeline {
    agent any

    environment {
        CONFLUENCE_BASE_URL = 'https://your-confluence-site.atlassian.net/wiki'
        CONFLUENCE_USERNAME = 'carmenappelt26@gmail.com'
        CONFLUENCE_API_TOKEN = 'ATATT3xFfGF01x-2OBx0yVDQwQiEluTrr0J6Tgpu2dghAIF5TNN-tKEnAmOnGz7DqTKwWF6YPVP4p7wXpxqNxWwHpgOP-gDZDML9mmrs4SJOM2ZJT-VrTePnPYm3p8Eu7iXJn0vmhFLCPWlzl4FRMfjgSQdQc3RgDpQKvPTZZ8LbKlebvLoK5qA=E76B0048'
        PAGE_ID = '98408' // Die ID der Confluence-Seite, auf der der Anhang hochgeladen werden soll
        FILE_TO_UPLOAD = './image.png'
    }

    stages {
        stage('Checkout Repository 2') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: "https://github.com/carmenappelt/confluence.git"]]
                ])
            }
        }
        stage('Upload File to Confluence') {
            steps {
                script {
                    def response = sh script: """
                        curl -u $CONFLUENCE_USERNAME:$CONFLUENCE_API_TOKEN -X POST -H 'X-Atlassian-Token: no-check' \\
                        -F 'file=@image.png' \\
                        "${env.CONFLUENCE_BASE_URL}/rest/api/content/${env.PAGE_ID}/child/attachment"
                    """, returnStdout: true
                    println("Response: ${response}")
                }
            }
        }
    }
}
