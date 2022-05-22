pipeline {
    agent any
   
   environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

    options { buildDiscarder(logRotator(artifactDaysToKeepStr: '',
     artifactNumToKeepStr: '', daysToKeepStr: '3', numToKeepStr: '5'))
      disableConcurrentBuilds() }
      

    stages {
        
       stage('Setup parameters') {
            steps {
                script { 
                    properties([
                        parameters([
                          

                            string(
                                defaultValue: '001', 
                                name: 'ImageTAG', 
                                trim: true
                            )
                        ])
                    ])
                }
            }
        }




        stage('clean') {
            agent {
                 docker { image 'maven:3.8.5-openjdk-8-slim' }
             }

            steps {
               sh '''
               rm -rf webapp/target/webapp.war || true
