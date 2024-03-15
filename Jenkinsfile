pipeline {
    agent any
    environment{
        DOCKERHUB_CREDS = credentials('dockerhub')
    }

    stages {
        stage('Unit Test') {
            steps {
                script {
                        scm checkout
                        sh 'npm install'
                        sh 'npm test'
                        step([$class: 'JUnitResultArchiver', testResults: '**/test-results.xml'])  
                }
            }
        }

        stage('OWASP Check') {
            steps {
                script {

                        // Execute OWASP dependency check
                        sh 'npm audit --json > owasp-report.json'
                        // Publish OWASP report to Jenkins
                        stash includes: 'owasp-report.json', name: 'owaspReport'

                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                        // Build Docker image
                        sh 'docker build -t poomdechj/applab:${BUILD_NUMBER} .'
                        // Push Docker image to Docker registry
                        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                            sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        }
                        sh 'docker push poomdechj/applab:${BUILD_NUMBER}'
                }
            }
        }

    //    stage('Deploy to kind K8s') {
    //        steps {
    //            script {
    //                    // Deploy to Kubernetes using manifest, helm, or other method
    //                    // For simplicity, let's assume using kubectl apply with manifest files
    //                    sh 'kubectl apply -f k8s-manifests/' 
    //            }
    //        }
    //    }
    //}

    //post {
    //    always {
    //        // Archive artifacts
    //        dir('app') {
    //            archiveArtifacts artifacts: 'dist/**/*.js', fingerprint: true
    //        }
//
    //        // Publish HTML reports
    //        dir('app') {
    //            publishHTML(target: [
    //                allowMissing: false,
    //                alwaysLinkToLastBuild: false,
    //                keepAll: true,
    //                reportDir: 'coverage',
    //                reportFiles: 'index.html',
    //                reportName: 'Code Coverage Report'
    //            ])
    //        }
//
    //        // Publish OWASP report
    //        dir('app') {
    //            stash includes: 'owasp-report.json', name: 'owaspReport'
    //            archiveArtifacts artifacts: 'owaspReport/*', fingerprint: true
    //        }
    //    }
    //}
}
