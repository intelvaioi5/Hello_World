pipeline{
 agent {
    docker {
        image 'maven:3-alpine'
        args  '-v /tmp:/tmp'
    }
 }
 stages{
  stage("Build Stage"){
   steps{
    echo "This is build stage"
   }
  }
 }
}
