podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', command: 'cat', ttyEnabled: true),
	containerTemplate(name: 'buildkit', image: 'moby/buildkit:master', ttyEnabled: true, privileged: true),
  ]
  ) {
    node(POD_LABEL) {
        checkout scm

        stage('Maven hello') {
            container('maven') {
                sh 'mvn --version'
                sh 'mvn --version > mvn.version'
                archiveArtifacts artifacts: 'mvn.version', fingerprint: true
            }
        }

        stage('Build Docker Image') {
            container('buildkit') {
                sh 'ls -last'
                sh """
                  buildctl build --frontend gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --output type=image,name=docker.io/username/image:tag
                """
                milestone(1)
            }
        }
    }
}
