pipeline{
    agent any
     environment {
        EXAMPLE_CREDS = credentials('gitcred')
    }

    tools {
         maven 'mymvn'
         jdk 'java'
    }

    stages{
        // stage('checkout'){
        //     steps{
        //         checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]])
        //     }
        // }
        stage('pom') {
            steps{
                script{
                    def pom = readMavenPom file: 'pom.xml'
                    def version = pom.version
                    println "Version: ${version}"
                    def versionArray = version.split("[-|\\.]")
                    println "VersionArray: ${versionArray}"
                    fixed = versionArray[0]
                    major = versionArray[1]
                    minor = versionArray[2]
                    patch = versionArray[3]
                    ipatch = patch.toInteger()+1
                    fxsnap = versionArray[4]
                    def newpom = "${fixed}.${major}.${minor}.${ipatch}-${fxsnap}"
                    println "pomnewversion: ${newpom}"
                    // git remote add origin git@github.com:prasad-deepu/sample-java.git                                        
                    // sh 'git clone https://github.com/myusername/my-repo.git'
                    // git remote set-url origin https://prasad-deepu@github.com/prasad-deepu/sample-java.git 
                    //  sh"""
                    // #touch .gitignore
                    // echo "# Ignore everything\n*\n\n# Except for XML files\n!*.xml" > .gitignore   
                    // git commit -m "incremented patch version by 1"   
                    // withCredentials([usernamePassword(credentialsId: 'gitcred', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh""" 
                    rm -rf sample-java/
                    git clone https://github.com/prasad-deepu/sample-java.git
                    cd sample-java
                    git branch
                    mvn org.codehaus.mojo:versions-maven-plugin:2.15.0:set -DnewVersion=$newpom -DgenerateBackupPoms=false                    
                    git status 
                    git add pom.xml
                    git commit -m "incremented pom version to ${ipatch}"                   
                    git status             
                    git push 'https://${EXAMPLE_CREDS_USR}:${EXAMPLE_CREDS_PSW}@github.com/${EXAMPLE_CREDS_USR}/sample-java.git'
                    """    
                        // }
                                  
                }
            }
        }

        stage('build'){
            steps{
               sh 'echo building'
            }
        }
    }
}