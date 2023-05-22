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
                                    pip3 -v
                                    python3 --version
                                    apk add nodejs npm
                                """
        				    }
        				}
        			}
        		}
        	}
    	}
      stage ('Install node') {
    		steps {
        		dir("${workspace}") {
        			script {
        				script {
        				    container('docker-client') {
        					    sh"""
                                    npm --version
                                    npm install
                                    
                                """
        				    }
        				}
        			}
        		}
        	}
    	}
    stage ('build') {
    		steps {
        		dir("${workspace}") {
        			script {
        				script {
        				    container('docker-client') {
        					    sh"""
                                    docker images
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
