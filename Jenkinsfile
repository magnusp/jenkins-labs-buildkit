podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', command: 'cat', ttyEnabled: true),
	containerTemplate(name: 'buildkit', image: 'moby/buildkit:master', ttyEnabled: true, privileged: true),
  ]
  ) {
    node(POD_LABEL) {
        stage('Maven hello') {
            container('maven') {
                sh 'mvn --version'
                sh 'mvn --version > mvn.version'
                archiveArtifacts artifacts: 'mvn.version', fingerprint: true
            }
        }

        stage('Build Docker Image') {
            container('buildkit') {
                sh """
                  buildctl build --frontend=dockerfile.v0 --local context=. --local dockerfile=.
                """
                milestone(1)
            }
        }
    }
}
