pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/DongJunLee24/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t dongjunlee24/cicdtest:green2 . 
        sudo docker push dongjunlee24/cicdtest:green2
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deploy myweb2 --image=dongjunlee24/cicdtest:green2'
        ansible master -m command -a 'kubectl expose deploy myweb2 --type="LoadBalancer" --port=80 --target-port=80 --protocol="TCP"'
        '''
      }
    }
  }
}
