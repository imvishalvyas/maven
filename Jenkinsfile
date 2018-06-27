pipeline {
agent any
tools {
maven 'maven'
jdk 'java'
}
stages {
stage ('init') {
steps {
sh '''
echo "PATH = ${PATH}"
echo "M2_HOME = ${M2_HOME}"
'''
}
}
stage ('buid') {
steps {
sh '''
maven clean package checkstyle:checkstyle
'''
}
post {
success {
archiveArtifacts '**/*.war'
junit '**/target/surefire-reports/*.xml'
checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
}
}
}
stage ('Deploy') {
steps {
build 'Deploy'
}
}
}
}
