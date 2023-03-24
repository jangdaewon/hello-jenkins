node {
    env.REPO_URL = 'https://github.com/jangdaewon/hello-jenkins.git'
    env.BRANCH = 'main'
    env.APP_NAME = 'hello-jenkins'

    stage('Checkout') {
        echo "Checkout ${env.REPO_URL} on branch ${env.BRANCH}"
        git branch: "${env.BRANCH}", url: "${env.REPO_URL}"
    }

    stage('Build') {
        echo "Build ${env.APP_NAME}"
        withMaven(maven: 'Maven3', mavenLocalRepo: '.repository') {
            sh 'chmod +x ./mvnw'
            sh 'mvn clean install -DskipTests'
        }
    }

    stage("Deployment") {
        echo "Deploy ${env.APP_NAME}"
        sh 'nohup ./mvnw spring-boot:run -Dserver.port=9090 &'
    }
}