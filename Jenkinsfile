def label = "jnlp-slave"
podTemplate(label: label, cloud: 'kubernetes',containers: [
  containerTemplate(name: 'maven', image: 'maven:3.6-alpine', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'kubectl', image: 'cnych/kubectl', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'helm', image: 'cnych/helm', command: 'cat', ttyEnabled: true)
], volumes: [
  hostPathVolume(mountPath: '/root/.m2', hostPath: '/var/run/m2'),
  hostPathVolume(mountPath: '/home/jenkins/.kube', hostPath: '/root/.kube'),
  hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
  node(label) {
    def myRepo = checkout scm
    def gitCommit = myRepo.GIT_COMMIT
    def gitBranch = myRepo.GIT_BRANCH

    stage('testing') {
      echo "testing"
    }
    stage('build image') {
      container('docker') {
        echo "build docker images"
      }
    }
    stage('Kubectl') {
      container('kubectl') {
        echo "list pods"
        sh "kubectl get pods --all-namespaces"
      }
    }
    stage('Helm') {
      container('helm') {
        echo "helm init"
        sh "helm list"
      }
    }
  }
}
