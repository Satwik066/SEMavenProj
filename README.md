# selab-internal
{
    agent any
    tools{
        maven "MAVEN_HOME"
    }
    stages{
        stage("repo and clean"){
            stepipelineps{
                bat "rmdir /s /q SEMavenProj"
                echo "Cloning repo"
                bat "git clone https://github.com/Satwik066/SEMavenProj.git"
                bat "mvn clean -f SEMavenProj"
                echo "Cleaned"
            }
        }
        stage("install"){
            steps{
                bat "mvn install -f SEMavenProj"
                echo "Installed"
            }
        }
        stage("test"){
            steps{
                bat "mvn test -f SEMavenProj"
                echo "Test Successful"
            }
        }
        stage("deploy"){
            steps{
                bat "mvn package -f SEMavenProj"
                echo "Deployed"
            }
        }
    }
}
