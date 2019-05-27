node {
   def mvn1
   def app
   stage('Checkout') { 
      git 'https://github.com/paulsoumi96/springmvc-helloworld.git'
      mvn1 = tool 'MAVEN_HOME'
   }
stage ('Build') {
       sh "'${mvn1}/bin/mvn' -Dmaven.test.failure.ignore clean package"
   }

stage ('Docker Image Build') {
       app = docker.build("paulsoumi96/devops:${BUILD_NUMBER}")
}

stage ('Push Docker Image') {
       docker.withRegistry('https://registry.hub.docker.com','dockerCred') {
        		app.push("1-${BUILD_NUMBER}")
        		app.push("latest")
      	}
}

stage('Run Container') {
      sh "docker run -p 8084:8080 -d paulsoumi96/devops"
}

}
