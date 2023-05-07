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