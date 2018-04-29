properties([pipelineTriggers([githubPush()])])

node('linux') {

    git url: 'https://github.com/jacksbd2/java-project.git', branch: 'master'

    stage('Test') {
        sh "env"
        sh "ant -f test.xml -v"
    }
    
    stage('Build'){
        sh "ant -f build.xml -v" 
    }
    
    stage('Deploy'){
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
	}
    
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'bd92d205-9e6e-4376-8c30-518a058d1efa', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"}   
    }
    
}
