pipeline {
    agent any

    environment {
        GOROOT = '/tmp/jenkins_go/go'
    	PATH = "/tmp/jenkins_go/go/bin:$PATH"
	CUR_PATH = "${WORKSPACE}"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..dd'
		sh('pwd && ls && env')
            }
        }
        stage('Test') {
            steps {
		ws("${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_ID}/") {
   			withEnv(["GOPATH=${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_ID}/go"]) {
                		echo 'Testing..'
				sh('echo $USER && env')
				sh('mkdir go && mkdir go/src && mkdir go/src/project')
				sh('cp -R ${CUR_PATH}/* go/src/project')
				sh('ls ${WORKSPACE}')
				sh('wget https://storage.googleapis.com/golang/go1.9.1.linux-amd64.tar.gz')
				sh('rm -rf /tmp/jenkins_go && mkdir /tmp/jenkins_go')
				sh('tar -xzf go1.9.1.linux-amd64.tar.gz --directory /tmp/jenkins_go')
				sh('echo $PATH')
				sh('cd $GOPATH/src/project && ls && go version')
				sh('cd $GOPATH/src/project && go get ./...')
				sh('cd app && go test')
			}
		}
	    }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
