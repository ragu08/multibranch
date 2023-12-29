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

        stage('master') {
            when {
                branch "master"
            }

            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"

                echo "This is MASTER Branch"
                script {

                  // Run GitVersion
                       def gitversionOutput = sh(script: 'docker run --rm -v $WORKSPACE:/repo gittools/gitversion:latest /repo /output buildserver /l debug', returnStdout: true).trim()
                       echo "GitVersion Output: ${gitversionOutput}"
                       echo env.GitVersion_SemVer
                       echo env.GitVersion_MajorMinorPatch
                      echo env.GitVersion_FullSemVer


                }
            }
        }

        stage('development') {
            when {
                branch "development"
            }

            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"

                echo "This is DEVELOPMENT Branch"
                script {

                     // Run GitVersion
                       def gitversionOutput = sh(script: 'docker run --rm -v $WORKSPACE:/repo gittools/gitversion:latest /repo /output buildserver /l debug', returnStdout: true).trim()
                       echo "GitVersion Output: ${gitversionOutput}"
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
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"

                echo "This is FEATURE Branch"
                script {

                    // Run GitVersion
                       // Specify the GitVersion Docker image and version
                    def gitversionImage = 'gittools/gitversion:5.6.6'

                   // Run GitVersion and capture the output
                    sh "docker run --rm -v ${WORKSPACE}:/repo ${gitversionImage} /repo "


                    // Read GitVersion output from properties file
                    def props = readProperties file: '/repo/gitversion.properties'

                    // Set environment variables with GitVersion information
                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha

                }
            }
         }


        stage('bugfix') {
            when {
                branch "bugfix"
            }

            
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"

                script {

                    // Run GitVersion
                       def gitversionOutput = sh(script: 'docker run --rm -v $WORKSPACE:/repo gittools/gitversion:latest /repo /output buildserver /l debug', returnStdout: true).trim()
                       echo "GitVersion Output: ${gitversionOutput}"
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


                echo "This is RELEASE Branch"
                script {

                    // Run GitVersion
                       def gitversionOutput = sh(script: 'docker run --rm -v $WORKSPACE:/repo gittools/gitversion:latest /repo /output buildserver /l debug', returnStdout: true).trim()
                       echo "GitVersion Output: ${gitversionOutput}"
                       echo env.GitVersion_SemVer
                       echo env.GitVersion_MajorMinorPatch
                      echo env.GitVersion_FullSemVer


                }
            }
        }


    }

}

