pipeline {
    agent any

    environment {
        FLUTTER_HOME = "/usr/local/flutter"
        ANDROID_SDK_ROOT = "/android-sdk"
        FIREBASE_SERVICE_ACCOUNT_KEY = credentials('FIREBASE_SERVICE_ACCOUNT_KEY')
        JENKINS_USERNAME = "Ragunath"

    }

    stages{

        stage('Checkout') {
            when {
                branch "development"
            }
            steps {
                script {
                    checkout scmGit(branches: [[name: 'development']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/ragu08/Andorid_cicd.git']])
                }
            }
        }


        stage('branch name') {
            steps {
                echo "${env.BRANCH_NAME}"


                sh '''

                printenv

                '''

            }
        }

        stage('main') {
            when {
                branch "main"
            }

            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"


                sh '''

                printenv
                /root/.dotnet/tools/dotnet-gitversion /output buildserver

                '''

                echo "This is MAIN Branch"
                script {

                    def props = readProperties file: 'gitversion.properties'
                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha
                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer

                }
            }
        }

        stage('develop') {
            when {
                branch "development"
            }

            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"


                sh '''

                printenv
                /root/.dotnet/tools/dotnet-gitversion /output buildserver

                '''

                echo "This is DEVELOPMENT Branch"
                script {

                    def props = readProperties file: 'gitversion.properties'
                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha
                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer

                }
            }
        }

        stage('Build Flutter App') {
            when {
                branch  "development"
            }
            steps {
                script {
                    dir('/var/jenkins_home/workspace/demo-flutter_development') {        

                        // Run flutter doctor to check Flutter environment
                        sh 'sudo /usr/local/flutter/bin/flutter pub get'

                        // Run flutter build appbundle
                        sh 'sudo  /usr/local/flutter/bin/flutter build apk'

                    }

                }
            }

        }

        stage('Distribute to Firebase') {
            when {
                branch "development"
            }
            steps {
                script {
                    withCredentials([file(credentialsId: 'FIREBASE_SERVICE_ACCOUNT_KEY', variable: 'SERVICE_ACCOUNT_KEY')]) {
                        // Set GOOGLE_APPLICATION_CREDENTIALS environment variable
                        env.GOOGLE_APPLICATION_CREDENTIALS = env.SERVICE_ACCOUNT_KEY
                        // Activate service account using gcloud
                        sh "gcloud auth activate-service-account --key-file=${env.SERVICE_ACCOUNT_KEY}"
                        sh 'firebase appdistribution:distribute /var/jenkins_home/workspace/MWS-FLUTTER/testing_cicd/build/app/outputs/flutter-apk/app-release.apk --app "1:913095119574:android:ff47863d3b9ad110c22f77" --groups "test" --release-notes "updated file"'
                    }
                }
            }
        }

        stage('Office 365 Notification') {
            when {
                branch "development"
            }
            steps {
                script {
                    // Get build information
                    def buildNumber = env.BUILD_NUMBER
                    def buildStatus = currentBuild.currentResult ?: 'UNKNOWN'

                    // Use the git step to get the committer's name
                    def committerName = sh(script: 'git log -1 --pretty=format:%an', returnStdout: true).trim() ?: 'Unknown Committer'

                    // Build remarks based on start time
                    def remarks = "Started Jenkins pipeline by ${JENKINS_USERNAME}"



                    // Get webhook URL from secret using withCredentials
                    def webhookUrl
                    withCredentials([string(credentialsId: 'FERTECH-CICD', variable: 'WEBHOOK_URL')]) {
                        webhookUrl = env.WEBHOOK_URL
                    }

                    // Format message for Teams
                    def teamsMessage = """
                    Latest status of build #${buildNumber}
                    **Status:** BUILD ${buildStatus}
                    **Remarks:** ${remarks}
                    **Committers:** ${committerName}
                    **Developers:** ${committerName}
                    """

                    // Send message to Office 365 using webhook URL
                    office365ConnectorSend message: teamsMessage.trim(),
                    //status: 'SUCCESS', // Specify the status for success
                    webhookUrl: webhookUrl // Use the webhook URL directly

                }
            }
        }


        stage('feature') {
            when {
                branch "feature"
            }

            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"


                sh '''

                printenv
                /root/.dotnet/tools/dotnet-gitversion /output buildserver

                '''

                echo "This is FEATURE Branch"
                script {

                    def props = readProperties file: 'gitversion.properties'
                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha
                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer
                }
            }
        }


        stage('bugfix') {
            when {
                branch "bugfix"
            }

            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"


                sh '''

                printenv
                /root/.dotnet/tools/dotnet-gitversion /output buildserver

                '''

                echo "This is BUGFIX Branch"
                script {

                    def props = readProperties file: 'gitversion.properties'
                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha
                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer

                }
            }
        }


        stage('release') {
            when {
                branch "release"
            }

            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"


                sh '''

                printenv
                /root/.dotnet/tools/dotnet-gitversion /output buildserver

                '''

                echo "This is RELEASE Branch"
                script {

                    def props = readProperties file: 'gitversion.properties'
                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha
                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer

                }
            }
        }


    }

}
