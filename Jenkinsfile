pipeline{
    agent any

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
                    withCredentials([usernamePassword(credentialsId: 'gitcred', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh""" 
                    git checkout new3
                    mvn org.codehaus.mojo:versions-maven-plugin:2.15.0:set -DnewVersion="${newpom}" -DgenerateBackupPoms=false
                    git status 
                    git add pom.xml                    
                    git status             
                    git push "https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/sample-java.git" new3
                    """    
                        }
                                  
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