pipeline {
    agent any
    stages {
        stage('Check Out GIT repo') {
            steps {
                git branch: 'v2.0', url: 'https://github.com/ng-rh/employee-app-v2.git'
                
            }
            
        }
        stage('Login to a dev cluster') {
            steps {
                sh "oc login https://api.cluster-nn9bx.nn9bx.sandbox1323.opentlc.com:6443 --username=opentlc-mgr --password=r3dh4t1! --insecure-skip-tls-verify"
                
            }
            
        }
        stage('Login to namespace') {
            steps {
                sh "oc project pipeline"
                
            }
            
        }
        stage('Create Jenkins Service Account') {
            steps {
                sh "oc create sa jenkins-service-account"
                
            }
        }
        stage('Give access to the dev user') {
            steps {
                sh "oc policy add-role-to-user edit system:serviceaccount:default:jenkins-service-account -n pipeline"
                
            }
            
        }
        stage('Deploy v2 in Dev Env') {
            steps {
                sh "oc new-app employee-v1:latest~https://github.com/ng-rh/employee-app-v2.git#v2.0"
            }
            
        }
        stage('Expose the service for employee-v2 in Dev Env') {
            steps {
                sh "oc expose service employee-app-v2 -n pipeline"
                
            }
            
        }
        stage('Approve or Reject') {
            steps {
                input 'Approve?'
                
            }
        }
    }
}
