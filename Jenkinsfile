pipeline {
    agent {
        label 'ubuntu1804'
    }

    environment {
        APP_VERSION = '0.0.1'

        }

    stages {

        stage('Preparation') { 
            steps {
                print "DEBUG: parameter APP_VERSION   = ${APP_VERSION}"
                
                // Clean up the workspace, so we always start from a clean clone
                cleanWs()

                // Checkout source code from Git repo
                checkout scm
            }
        }

        stage('Build') {
            steps {
                print "DEBUG: Begin Build Step"

                docker build -t SONAR/sonar-app .

                print "DEBUG: End Build Step"
            }
        }

        stage('Results') {
            steps {
                sh 'echo "No testing means no results. Just running the deployment"'
            }
        }

        stage('Publishing'){
            steps {
                print "DEBUG: Begin Publishing Step"
                print "DEBUG: End Publishing Step"
            }
        }

        stage('Deploy Sonar_QA') {
            
            when {
                branch 'qa'
            }

            steps {
                sh 'echo "Use Rundeck to deploy to sonar_qa environment"'
                
//                step([$class: "RundeckNotifier",
//                    includeRundeckLogs: true,
//                    jobId: "48f0f25b-9c18-496f-a9f1-e3abfe9561de",
//                    nodeFilters: "",
//                    options: """
//                        UPDATE_WP_CORE=${UPDATE_WP_CORE}
//                        CONFIG_VERSION=${CORE_VERSION}
//                        """,
//                    rundeckInstance: "rundeck.devops.tchinternal.com",
//                    shouldFailTheBuild: true,
//                    shouldWaitForRundeckJob: true,
//                    tags: "",
//                    tailLog: true]
//                )
            }
        }

        stage('Deploy Sonar_Production') {
            
            when {
                branch 'master'
            }

            steps {
                sh 'echo "Use Rundeck to deploy to sonar_production environment"'
                
//                step([$class: "RundeckNotifier",
//                    includeRundeckLogs: true,
//                    jobId: "48f0f25b-9c18-496f-a9f1-e3abfe9561de",
//                    nodeFilters: "",
//                    options: """
//                        UPDATE_WP_CORE=${UPDATE_WP_CORE}
//                        CONFIG_VERSION=${CORE_VERSION}
//                        """,
//                    rundeckInstance: "rundeck.devops.tchinternal.com",
//                    shouldFailTheBuild: true,
//                    shouldWaitForRundeckJob: true,
//                    tags: "",
//                    tailLog: true]
/                )
            }
        }
    }
}