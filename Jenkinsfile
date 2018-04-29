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
	sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://jack3604-assignment-10/*.*"
    }
    
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'e00b8b1d-7e9f-405b-9ec6-d25c63325c5d', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    	sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'    
	}
    }
}
