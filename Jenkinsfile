podTemplate(containers: [
    containerTemplate(name: 'spec-toolkit', image: 'ghcr.io/magnusp/specification-toolkit:5', command: 'cat', ttyEnabled: true),
  ]
  ) {
    node(POD_LABEL) {
        checkout scm

        stage('The stage') {
            container('spec-toolkit') {
                sh 'oasdiff --version'
                sh 'vacuum version'
            }
        }
    }
}
