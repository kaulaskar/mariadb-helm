pipeline{
  agent any
  stages{
  //   stage('connecting to cluster'){
  //     steps{
  //     sh 'kubectl config use-context arn:aws:eks:us-west-2:897276212041:cluster/devops-eks-gCFGYxzJ'
  //     }
  // }
    // stage('clean workspace'){
    //  steps{
    //   deleteDir()
    //  }
    // }
    stage('create db namespace'){
      steps{
       sh '''
        myNamespace="database"
        sudo kubectl get namespace | grep -q "^$myNamespace " || sudo kubectl create namespace $myNamespace
         '''
    }
    }
  stage('deploy mariadb'){
    steps{
    sh 'sudo helm upgrade --install mariadb $WORKSPACE --values $WORKSPACE/createat-mariadb.yaml --namespace database '
    }
  }
 stage('pod status'){
   steps{
   sh 'sudo kubectl get pods -n database'
   }
 }
    
}
}
