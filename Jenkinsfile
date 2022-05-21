pipeline {    
    agent any    
    tools {   
        maven 'maven-3.8'   
    }   
        stages {    
            stage("git_checkout") {    
                steps {    
                    echo "cloning repository"   
                    git branch: 'J2EE', url: ' https://github.com/Ajith87907/onlinebookstore.git '    
                    echo "repo cloned successfully"    
                    }    
                }    
            stage("building_code") {    
                steps {    
                    sh 'mvn clean package'    
                    // rename package name   
                    sh 'mv **/*.war target/bookstore.war'   
                }    
            }    
            stage("deploy") {   
                steps {   
                    // under here mention your credentials of tomcat server    
                    sshagent(['tomcat8'])  
                        {   
                            sh """    
                            scp -o StrictHostKeyChecking=no target/bookstore.war ec2-user@3.85.201.201:/opt/tomcat8/webapps/   
                            ssh ec2-user@3.85.201.201 /opt/tomcat8/bin/shutdown.sh   
                            ssh ec2-user@3.85.201.201 /opt/tomcat8/bin/startup.sh   
                            """   
                        }   
                }   
            }   
        }   
    } 
