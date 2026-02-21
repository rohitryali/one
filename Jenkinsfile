pipeline {
    agent {
        node {
            label "test"
        }
    }
    triggers {
        githubPush()
    }
    tools {
        maven "mymaven"
    }
    stages {
        stage("code"){
            steps{
                git branch: 'rohit', url: 'https://github.com/rohitryali/one.git'
            }
        }
        stage("build"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("artifact"){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/myweb-8.7.2.war', type: 'war']], credentialsId: '4f3945d6-2b63-4bc3-9752-7c268c01c8fd', groupId: 'in.javahome', nexusUrl: '34.203.35.143:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'rohitrepo', version: '8.7.2'
            }
        }
        stage("deploy") {
            steps {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '8d28fe82-3533-46c9-a947-936c5c1364ed', path: '', url: 'http://34.224.87.246:8080/')], contextPath: 'muwebsite', war: 'target/*.war'
            }
        }
    }
}
