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
                                    pip install checkov
                                    python3 --version
                                    apk add nodejs npm
                                   
                                """
        				    }
        				}
        			}
        		}
        	}
    	}
      stage ('Install nodejs') {
    		steps {
        		dir("${workspace}") {
        			script {
        				script {
        				    container('docker-client') {
        					    sh"""
                                    npm --version
                                    npm install
                                    npm run build
                                    
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
                                    docker swarm init
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
stage('Push image to JFrog') {
steps {
withCredentials([(credentialsId: 'a4dcccc4-57ce-44ff-8386-38d1a45e6d8c')])
   dir("${workspace}") {
        			script {
        				script {
        				    container('docker-client') {
        					    sh"""
                                   docker push dsaf.jfrog.io/images/jenkins-react
                                """
        				    }
        				}
        			}
        		}
