pipeline{
    agent any
        stages{
		stage('Git Clone'){
            steps{
                git branch: 'main', url: 'https://github.com/Rameshagwd/nexus_pipeline.git'
            }
        }
		stage('MVN Clen'){
            steps{
                sh 'mvn clean'
            }
        }
        
        stage('Maven Compile'){
            steps{
                sh 'mvn compile'
            }
        }
		stage('Maven validate'){
            steps{
                sh 'mvn validate'
            }
        }
        stage('Maven Test'){
            steps{
                sh 'mvn test'
            }
        }   
        stage('Maven package'){
            steps{
                sh 'mvn package'
            }
        }
		stage('Upload Jar to Nexus'){
            steps{
                scirpt{
                 def mavenpom = readMavenPom file: 'pom.xml'
                 nexusArtifactUploader artifacts: [
                     [
                        artifactId: 'nexus_pipeline',
                        classifier: '',
                        file: "target/nexus_pipeline-${mavenPom.version}.jar",
                        type: "jar"
                        ]
                    ],
                    credentialsId: 'nexus',
                    groupId: 'com.javatpoint.application1',
                    nexusUrl: '10.32.39.203:8081',
                    nexusVersion: 'nexus3',
                    protocal: 'http',
                    repository: 'release-repo',
                    version: "${mavenPom.version}" 

                    
                }
            }
        }
        
        
    }
}