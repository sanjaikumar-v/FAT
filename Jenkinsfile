node {
    stage('Checkout GITHUB') {
        checkout scm
    }
    stage('Create Docker image') {
        sh 'docker build -t sanjaikumar1one /movie-rating:latest .'
    }
    stage('Push to Docker Hub') {
        withCredentials([usernamePassword(credentialsId: 'docker-hub-login', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
            sh 'echo \ | docker login -u \ --password-stdin'
            sh 'docker push sanjaikumar1one /movie-rating:latest'
        }
    }
    stage('Create Cluster in Kubernetes') {
        sh 'kubectl apply -f deployment.yaml'
    }
    stage('Show deployed application') {
        sh 'kubectl get svc movie-service'
    }
}
