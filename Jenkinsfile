def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(
        name: 'kubectl',
        image: 'seldonio/k8s-deployer:k8s_v1.14.0',
        command: 'cat',
        ttyEnabled: true,
        envVars: [
            secretEnvVar(key: 'GITHUB_USER', secretName: 'github-credentials', secretKey: 'user'),
            secretEnvVar(key: 'GITHUB_TOKEN', secretName: 'github-credentials', secretKey: 'token')
        ]),
],
volumes: [
  hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
  node(label) {

    def myRepo = checkout scm
    def gitCommit = myRepo.GIT_COMMIT
    def gitBranch = myRepo.GIT_BRANCH

    stage('activity-monitor') {
      container('kubectl') {
        sh "curl -s activity-monitor.default.svc.cluster.local:80/?'(JENKINS) build-model-images-job run for v'${BUILD_ID} > /dev/null"
      }
    }
    stage('build-model') {
      container('kubectl') {
        sh 'pwd'
        sh 'ls -al'
        sh "make -f Makefile.build-model-images-job do_build MODEL_VERSION=v${BUILD_ID}"
      }
    }
  }
}
