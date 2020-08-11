pipeline {
    agent any

    environment {
        dotnet = 'C:\\Program Files (x86)\\dotnet\\'
    }

    triggers {
        pollSCM '* * * * *'
    }

    stages {
        stage ('checkout')){
            steps {
                git credentialsId: '', url: 'https://github.com/sajjasgit/mvc-core-docker-to-ecs.git', branch: 'master'
            }
        }

        stage ('restore packages') {
            steps {
                bat "dotnet restore WebApplication1\\WebApplication1.csproj"
            }
        }

        stage ('clean package') {
            steps {
                bat "dotnet clean WebApplication1\\WebApplication1.csproj"
            }
        }

        stage ('Build package') {
            steps {
                bat "dotnet build WebApplication1\\WebApplication1.csproj --configuration Release"
            }
        }
    }
}