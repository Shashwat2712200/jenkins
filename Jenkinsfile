pipeline {
   agent {
      kubernetes {
            defaultContainer 'jnlp'
            yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: cfdevsecopsNode
spec:
  containers:    
  - name: docker-client
    image: docker:dind
    tty: true
    securityContext:
      privileged: true
    env:
      - name: DOCKER_TLS_CERTDIR
        value: ""
'''
        }
   }
   stages{
   stage ('Install-Dependency') {
    		steps {
        		dir("${workspace}") {
        			script {
        				script {
        				    container('docker-client') {
        					    sh"""
                                    apk add py3-pip
                                    python3 --version
                                """
        				    }
        				}
        			}
        		}
        	}
    	}
    stage ('Install-Dependency') {
    		steps {
        		dir("${workspace}") {
        			script {
        				script {
        				    container('docker-client') {
        					    sh"""
                                    docker build -t jenkins-react .
                                """
        				    }
        				}
        			}
        		}
        	}
    	}
   }
}
