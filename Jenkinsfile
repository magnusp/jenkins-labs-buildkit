podTemplate(containers: [

    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', command: 'cat', ttyEnabled: true),

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
    }
}
