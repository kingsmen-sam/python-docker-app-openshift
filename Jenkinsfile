node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'satyagit', url: 'https://github.com/kingsmen-sam/python-docker-app-openshift.git'
      }
   
 stage('Docker Build') {
    def app = docker.build "satyasaipavan/python-app"
   }
   
   stage("Tag & Push image"){
      withDockerRegistry(credentialsId: 'dockcred', url: 'https://cloud.docker.com/repository/docker/satyasaipavan/python-app')  {
          sh 'docker tag satyasaipavan/python-app satyasaipavan/python-app:dev'
          sh 'docker push satyasaipavan/python-app:dev'
          sh 'docker push satyasaipavan/python-app:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=YWDIj1NLdNIDgOBX332PXBbi4sMYbdVUCr5JszKlR9U --server=https://api.us-west-1.starter.openshift-online.com:6443'
     sh 'oc project python-app'
     sh 'oc new-app --name python-app satyasaipavan/python-app'
      sh 'oc rollout latest dc/python-app -o json' 
     // sh 'oc rollout latest manee2k6/py-newrelic --name python \
         // --env NEWRELIC_LICENSE=a1869158b60fb11bebfa72898accacd1c76a7fe1 \
          //      NEWRELIC_APPNAME=PyApp-Newrelic'
     //sh 'oc expose svc py-mani' 
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }

  }
