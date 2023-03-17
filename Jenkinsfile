pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '955a1419-3757-4b72-893c-2b38c9e51168', path: '', url: 'http://172.31.19.64:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
            
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                input message: 'Approval from DM', submitter: 'srinivas'
                deploy adapters: [tomcat9(credentialsId: '955a1419-3757-4b72-893c-2b38c9e51168', path: '', url: 'http://172.31.28.43:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}
