pipeline {
	agent any 
	
	parameters {
  		string defaultValue: 'DEV', name: 'ENV'
	}
	
	triggers {
  		pollSCM '* * * * *'
	}
	
	stages {
	    stage('Checkout') {
	        steps {
			checkout scm			       
		      }}
		stage('Build') {
	           steps {
			  sh '/home/shivani/Documents/devops/apache-maven-3.9.6/bin/mvn install'
        }}
	    stage('Deployment'){
		    steps{
			script{
			 if ( env.ENV == 'QA' ){
        	sh 'cp target/red3.war /home/shivani/Documents/devops/apache-tomcat-9.0.88/webapps'
         echo "deployment has been COMPLETED on QA!"
			 }
			else ( env.ENV == 'UAT' ){
    		sh 'cp target/red3.war /home/shivani/Documents/devops/apache-tomcat-9.0.88/webapps'
        echo "deployment has been done on UAT!"
			}      
			}}}
		    stage('slack'){
			    steps{
				    slackSend baseUrl: 'https://hooks.slack.com/services /', channel: 'shivdemo1', color: 'good', teamDomain: 'abc', tokenCredentialId: 'shivdemo1', username: 'shivdemo1'
                                   }}
}}

	        
