pipeline{
agent {label 'slave'}
stages{
stage('git'){

steps{

checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'fbee8257-4320-4170-a2cc-53ea0974a7d9', url: 'https://github.com/devopschandu1/mavenrepo.git']]])
      }
           } // stage1 close
stage('maven'){

steps{
sh 'mvn package'
}
}

stage('sonar'){

steps{
withSonarQubeEnv('mysonarqubeserver') {
sh 'mvn sonar:sonar'
}

}

}

stage('nexus'){
steps{
sh 'mvn deploy'
}
}

stage('deploy'){
steps{
sh 'scp /root/workspace/maven/target/studentapp-2.5-SNAPSHOT.war 13.127.93.198:/var/lib/tomcat/webapps'
}
}
       }   // stages close
        }       // piepeline
