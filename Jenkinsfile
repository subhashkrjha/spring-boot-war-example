pipeline {
    agent any
     tools {
        maven 'MAVEN_JENKINS' 
        }
    stages {
        stage("Test"){
            steps{
                slackSend channel: 'devops-class', message: 'Job Started(Jenkins)'
                // mvn test
                //sh "mvn test"
                bat 'mvn test'
                //slackSend channel: 'youtubejenkins', message: 'Job Started'
                             
            }
            
        }
        stage("Build"){
            steps{
                //sh "mvn package"
                bat 'mvn package'
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                //deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://192.168.0.118:8080')], contextPath: '/app', war: '**/*.war'
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://localhost:8082')], contextPath: '/app', war: '**/*.war'
              
            }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container -> plugin
                //deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://192.168.0.119:8080')], contextPath: '/app', war: '**/*.war'
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://localhost:8082')], contextPath: '/app', war: '**/*.war'

            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
             //slackSend channel: 'youtubejenkins', message: 'Success'
             slackSend channel: 'devops-class', message: 'Job finished Successfully(Jenkins)'
        }
        failure{
            echo "========pipeline execution failed========"
             //slackSend channel: 'youtubejenkins', message: 'Job Failed'
             slackSend channel: 'devops-class', message: 'Job failed(Jenkins)'
        }
    }
}
