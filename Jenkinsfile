pipeline {
        agent any
		
		stages {
		   
		  stage("Git cLone"){
		          steps {
                           git  'https://github.com/AhmedAtefGaber/CI-CD/'
						}
                            }
    
  /*        stage("maven clean build"){
		          steps {
                           script {def mavenHome = tool name: "maven-3.6.3" , type: "maven"
                                   def mavenCMD  = "${mavenHome}/bin/mvn"}
                           sh "${mavenCMD} clean package"
                        }
                                     }
*/



          stage("maven clean build"){
                          steps {
 					 sh 'mvn -B -DskipTests clean package'
                        }
                                     }


          stage("build docker image"){
		          steps {
                           sh "docker build -t ahmedatefosman/sprint-boot-mongo ."
						}
                                     }

          stage("docker push"){
		          steps {
                           withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_pass')]) {
                           sh "docker login -u ahmedatefosman -p ${docker_pass} "
						                                                                                    }
                              
                           sh "docker push ahmedatefosman/sprint-boot-mongo "
						}
                              }

          stage("deploy on kubernetes cluster"){
		          steps {
                          /*
                          kubernetesDeploy(
                          configs: 'springBootMongo.yml',
                          kubeconfigId: 'k8s_config',
                          enableConfigSubstitution: true
                                           )
        */
                          sh "kubectl apply -f springBootMongo.yml "
	                    }
                                                  }

                       }
 }
