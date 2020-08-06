node('master') {
    stage('ContinuousDownload') {
        git 'https://github.com/intelliqittrainings/maven.git'
    }
    stage('ContinuousBuild') {
        sh label: '', script: 'mvn package'
    }
    stage('ContinuousDeployment') {
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.32.105:/var/lib/tomcat8/webapps/testApp.war'
    }
    stage('ContinuousTesting') {
        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
        sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
    }
    stage('ContinuousDelivery') {
        input message: 'Waiting for approval from DM', submitter: 'munni'
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.14.150:/var/lib/tomcat8/webapps/testApp.war'
    }
}