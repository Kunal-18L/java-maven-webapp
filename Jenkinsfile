pipeline {
    agent any
    
    tools {
        jdk 'jdk21'
        maven 'maven'
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Kunal-18L/java-maven-webapp.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=java-maven-webapp \
                    -Dsonar.host.url=$SONAR_HOST_URL \
                    -Dsonar.token=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }
        
        stage('Build DOcker Image') {
            steps {
                sh 'docker build -t java-maven-webapp:latest .'
            }
        }
        
        stage('Tag Docker Image') {
            steps {
                sh 'docker tag java-maven-webapp:latest kunal18l/java-maven-webapp:latest'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push kunal18l/java-maven-webapp:latest
                    docker logout
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no -i /var/lib/jenkins/.ssh/aws-linux.pem ubuntu@3.110.88.62 << '
                cd ~/devops-automation/kubernetes
                kubectl apply -f deployment.yml
                kubectl apply -f service.yaml
                '
                '''
            }
        }
    }
}
