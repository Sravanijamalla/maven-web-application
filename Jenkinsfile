node{
    
    def mavenHome = tool name: "Maven3.8.3"
    stage('CheckOutCode'){
       git branch: 'development', credentialsId: 'a449d8b1-55ab-4d1a-9412-033ebb5cdd57', url: 'https://github.com/Sravanijamalla/maven-web-application.git'
    }
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    /* stage('ExecuteSonarqubeReport'){
	    sh "${mavenHome}/bin/mvn clean sonar:sonar" 
	 }*/
	 stage('UploadArtifactIntoNexusServer'){
	    sh "${mavenHome}/bin/mvn clean deploy"
	 }
	 stage('DeploytheAppintoTomcat'){
	    sshagent(['234a1f73-fbb7-46c7-8409-dd8c24b6dd02']){
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.218.131.41:/opt/tomcat9/webapps"
        }
	 }
	 stage('Email Notification'){
	    emailext attachLog: true, body: '''Build Success


        Regards,
        Sravani''', replyTo: 'sravanij2116@gmail.com', subject: 'Build Success...!', to: 'sravani.jamalla@gmail.com'
	}
}
