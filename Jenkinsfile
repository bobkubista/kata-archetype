// Built by the kvm-server Jenkins (Kubernetes agent pods, one build at a time).
// 'mvn verify' runs the archetype integration test: it generates a kata from
// the archetype (src/test/resources/projects/basic) and runs 'mvn verify' on it.
pipeline {
  agent {
    kubernetes {
      defaultContainer 'maven'
      yaml '''
        spec:
          containers:
            - name: maven
              image: maven:3.9.16-eclipse-temurin-25
              command: ["cat"]
              tty: true
              resources:
                requests: { memory: 768Mi, cpu: 250m }
                limits: { memory: 1Gi }
      '''
    }
  }
  options {
    timestamps()
    disableConcurrentBuilds()
    buildDiscarder(logRotator(numToKeepStr: '10'))
    timeout(time: 30, unit: 'MINUTES')
  }
  stages {
    stage('Build and test the archetype') {
      steps {
        sh 'mvn -B -ntp verify'
      }
    }
  }
}
