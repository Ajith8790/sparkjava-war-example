pipeline {    
    agent any    
    tools {   
        maven 'maven'   
    }   
        stages {    
            stage("git_checkout") {    
                steps {    
                    echo "cloning repository"   
                    git branch: 'master', url: ' https://github.com/Ajith8790/sparkjava-war-example.git'    
                    echo "repo cloned successfully"    
                    }    
                }    
            stage("building_code") {    
                steps {    
                    sh 'mvn clean package'    
                    // rename package name   
                    sh 'mv **/*.war target/hello.war'   
                }    
            }    
            stage("deploy") {   
                steps {   
                    // under here mention your credentials of tomcat server    
                    sshagent(['tomcat2'])  
                        {   
                            sh """    
                            scp -o StrictHostKeyChecking=no target/hello.war ubuntu@18.212.227.221:/opt/apache-tomcat-8.5.78/webapps/   
                            ssh ubuntu@18.212.227.221 /opt/apache-tomcat-8.5.78/bin/shutdown.sh   
                            ssh ubuntu@18.212.227.221 /opt/apache-tomcat-8.5.78/bin/startup.sh   
                            """   
                        }   
                }   
            }   
        }   
    } 
