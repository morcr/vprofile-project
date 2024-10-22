pipeline {
  agent any
  tools {
    maven "MAVEN3"
    jdk "OracleJDK8"
  }
  
  environment {
    SNAP_REPO = "vprofile-snapshot"
    NEXUS_USER = "admin"
    NEXUS_PASS = "admin123"
    RELEASE_REPO = "vprofile-release"
    CENTRAL_REPO = "vpro-maven-central"
    NEXUSIP = "172.31.85.241"
    NEXUSPORT = "8081"
    NEXUS_GRP_REPO = "vprofile-maven-group"
    NEXUS_LOGIN = "nexuslogin"
  }
  stages {
    stage("test") {
      steps {
        sh "mvn -s settings.xml -DskipTests install"
      }
      post {
        success {
          echo "Now archiving."
          archiveArtifacts artifacts: '**/*.war'
        }
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    
    stage('Checkstyle Analysis') {
      steps {
        sh 'mvn checkstyle:checkstyle'
      }
    }
  }
}
