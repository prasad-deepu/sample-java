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
                    sh (script: "mvn org.codehaus.mojo:versions-maven-plugin:2.15.0:set -DnewVersion=${newpom} -DgenerateBackupPoms=false")
                    sh"""
                    git checkout -b new
                    git add pom.xml
                    git commit -m "incremented patch version by 1"  
                    git branch 
                    git remote -v                 
                    git push --set-upstream origin new
                    """                   
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