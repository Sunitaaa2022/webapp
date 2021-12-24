pipeline {
    agent any
    tools { 
        maven 'jenkins-maven' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }   
	 stage('Build') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }    
        }

        stage('Dependency Check') {
            steps {
               dependencyCheck additionalArguments: ''' 
                    -o "./" 
                    -s "./"
                    -f "ALL" 
                    --prettyPrint''', odcInstallation: 'depcheck'

                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }    
        }


		stage('Deploy') {
            steps {
                sh ' echo deployed'
               // deploy adapters: [tomcat9(credentialsId: '58b982ac-1e15-457d-a4e7-4ac39f1b2b21',path: '', url: 'http://192.168.1.9:8888/')], contextPath: 'testapp', war: '**/*.war'
            }  
        }
    }
}
