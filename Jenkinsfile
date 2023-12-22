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
                echo "${env.BRANCH_NAME}"/tmp/s
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
                       def gitversionOutput = sh(script: 'docker run --rm -v $WORKSPACE:/repo gittools/gitversion:latest /repo /output buildserver /l debug', returnStdout: true).trim()
                       echo "GitVersion Output: ${gitversionOutput}"
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

