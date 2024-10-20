node {
    def app
    stage('Clone repository') {
        git 'https://github.com/crolvlee/fork_vs_vfork.git'
    }
    stage('Build image') {
        app = docker.build("crolvlee/test")
    }
    stage('Test image') {
        app.inside {
            sh 'make test'
        }
    }
    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'crolvlee') {
           app.push("${env.BUILD_NUMBER}")
           app.push("latest")
        }
    }
}