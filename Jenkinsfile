node {
    stage("Checkout GITHUB") {
        checkout scm
    }
    stage("Test using JUNIT testing") {
        bat "mvn test"
    }
    stage("Build using Maven") {
        bat "mvn clean package"
    }
    stage("Create Docker image") {
        withEnv(["DOCKER_BUILDKIT=0"]) {
            bat "docker build -t sanjaikumar1one/movie-rating:latest ."
        }
    }
    stage("Push to Docker Hub") {
        withCredentials([usernamePassword(credentialsId: "docker-hub-login", passwordVariable: "PASS", usernameVariable: "USER")]) {
            // Using double quotes around variables to handle special characters
            bat "docker login -u %USER% -p %PASS%"
            bat "docker push sanjaikumar1one/movie-rating:latest"
        }
    }
    stage("Create Cluster in Kubernetes") {
        bat "kubectl apply -f deployment.yaml"
    }
    stage("Show deployed application") {
        bat "kubectl get svc movie-service"
    }
}