pipeline {
   
    agent {
            kubernetes {
            //cloud 'kubernetes'
            defaultContainer 'node'
            namespace 'default'
            yaml ''' 
            apiVersion: v1
            kind: Pod
            spec:
                containers:
                - name: node
                  image: node:20.11.1-alpine3.19
                  command:
                  - cat
                  tty: true
            '''
            }
        }
    environment {
        JAVA_HOME = tool name: 'JAVA', type: 'jdk' // Set JAVA_HOME to the JDK tool configured in Jenkins Global Tool Configuration
    }
    //environment{
    //    DOCKERHUB_CREDS = credentials('dockerhub')
    //}

    stages {
        stage('Unit Test') {
            //agent{
            //    kubernetes {
            //    //cloud 'kubernetes'
            //    defaultContainer 'node'
            //    namespace 'default'
            //    yaml ''' 
            //    apiVersion: v1
            //    kind: Pod
            //    spec:
            //        containers:
            //        - name: node
            //          image: node:20.11.1-alpine3.19
            //          command:
            //          - cat
            //          tty: true
            //    '''
            //    }
            //}
            steps {
                    dir('app'){
                //script {
                        //checkout scm
                        sh 'npm install'
        //                sh 'node --version'
        //                sh 'npm run test:ci'
        //                junit 'coverage/junit.xml'
        //                //sh 'npm run test:unit'
        //                //sh 'npm run lint'
        //                //sh 'npm ci:test'
        //                //step([$class: 'JUnitResultArchiver', testResults: '**/test-results.xml'])  
        //        //}
                    }
            }
        }
//
        stage('OWASP Check') {
            //agent {
            //    kubernetes {
            //        defaultContainer 'node'
            //        namespace 'default'
            //        yaml '''
            //        apiVersion: v1
            //        kind: Pod
            //        spec:
            //            containers:
            //            - name: node
            //              image: node:14
            //              command:
            //              - cat
            //              tty: true
            //    '''
            //    }
            //}
            steps {
                    dir('app'){

                    //sh "$JAVA_HOME/bin/java -jar dependency-check.jar -o 'owasp' -s 'package-lock.json' -f 'HTML' --prettyPrint"
                        
                        //sh 'npm install'
                        sh 'npm i owasp-dependency-check'
                        sh 'npm run owasp-test'
                     //script {
                    //dependencyCheck additionalArguments: ''' 
                    //            -o 'owasp'
                    //            -s 'package-lock.json'
                    //            -f 'HTML' 
                    //            --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
        //
                    //dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                        //sh 'dependency-check.sh --scan /workspace --format ALL --out /workspace/reports'
                    //    archiveArtifacts 'reports/**'
                        // Execute OWASP dependency check
                        //sh 'npm audit --json > owasp-report.json'
                        // Publish OWASP report to Jenkins
                        //stash includes: 'owasp-report.json', name: 'owaspReport'

                //}
                    }
                }
            }
//
    //    stage('Build Docker Image') {
    //        steps {
    //            //script {
    //                    // Build Docker image
    //                    sh 'docker build -t poomdechj/applab:$BUILD_NUMBER .'
    //                    // Push Docker image to Docker registry
    //                    //withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
    //                        //sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
    //                    //}
    //                    //sh 'docker login -u $DOCKERHUB_CREDS_USR -p $DOCKERHUB_CREDS_PSW'
    //                    sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
    //                    sh 'docker push poomdechj/applab:$BUILD_NUMBER'
    //            //}
    //        }
    //    }

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
}