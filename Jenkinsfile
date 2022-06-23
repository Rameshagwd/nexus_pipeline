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
                script {
                    pom = readMavenPom file: 'pom.xml'                                                      
                    nexusArtifactUploader artifacts: [
                        [
                             
                             artifactId: 'nexus_pipeline',
                             classifier: '',
                             file: "target/nexus_pipeline-${pom.version}.jar",
                             type: 'jar'
                        ]

                    ],

                    credentialsId: 'admin',
                    groupId: 'com.javatpoint.application1',
                    nexusUrl: '10.32.39.203:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'release-repo',
                    version: "${pom.version}" 

                }
                                 
                
            }
        }
        
        
    }
}