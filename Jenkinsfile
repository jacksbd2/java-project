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
	    sh "cp /workspace/java-pipeline/dist/rectangle-*.jar s3://jack3604-assignment-10/*.*"

    
}
