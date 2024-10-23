pipeline {
    agent any

    triggers{
        pollSCM("* * * * *")
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            parallel {
                stage('Run TestProject1 Tests') {
                    steps {
                        {
                            bat 'dotnet test TestProject1\\TestProject1.csproj --no-build --verbosity normal'
                        }
                    }
                }
                stage('Run TestProject2 Tests') {
                    steps {
                        {
                            bat 'dotnet test TestProject2\\TestProject2.csproj --no-build --verbosity normal'
                        }
                    }
                }
                stage('Run TestProject3 Tests') {
                    steps {
                        {
                            bat 'dotnet test TestProject3\\TestProject3.csproj --no-build --verbosity normal'
                        }
                    }
                }
            }
        }
    }
}
