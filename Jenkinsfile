pipeline {
    agent any

    stages{
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


        stage('feature') {
            when {
                branch "feature"
            }

            steps {
l                echo "${env.BRANCH_NAME}"
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

                gitversion /repo

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
