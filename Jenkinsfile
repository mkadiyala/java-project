pipeline {
  agent none

  stages {

    stage ('Unit Tests') {
      agent {
        label 'apache'
      }
      steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
    }

    stage('build') {
      agent {
        label 'apache'
      }
      steps {
        sh 'ant -f build.xml -v'
      }
    }

    stage('deploy') {
      agent {
        label 'apache'
      }
      steps {
        sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangle/all/"
      }
    }

    stage('deploy') {
      agent {
        label 'CentOS'
      }
      steps {
        sh "wget http//192.168.0.50/rectangle/all/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      }
    }
  }

post {
    always {
      archiveArtifacts artifacts: 'dist/*.jar', fingerprint:true
    }
  }
}
