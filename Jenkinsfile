pipeline {
    agent {
        label 'win1'
    }

    environment {
        dotnet = 'C:\\Program Files (x86)\\dotnet\\'
    }

    triggers {
        pollSCM '* * * * *'
    }

    stages {
        stage ('checkout') {
            steps {
                git credentialsId: 'da209a9d-3c28-40d8-a59e-cdc152009ea2', url: 'https://github.com/sajjasgit/mvc-core-docker-to-ecs.git', branch: 'origin/master'
            }
        }

        stage ('restore packages') {
            steps {
                bat "dotnet restore mvc-core-docker-to-ecs\\WebApplication1.csproj"
            }
        }

        stage ('clean package') {
            steps {
                bat "dotnet clean mvc-core-docker-to-ecs\\WebApplication1.csproj"
            }
        }

        stage ('Build package') {
            steps {
                bat "dotnet build mvc-core-docker-to-ecs\\WebApplication1.csproj --configuration Release"
            }
        }

        stage ('Publish package') {
            steps {
                bat "dotnet publish mvc-core-docker-to-ecs\\WebApplication1.csproj"
            }
        }
    }

    post {
        always {
            emailext body: "${currentBuild.currentResult}: Job   ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
            subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
}