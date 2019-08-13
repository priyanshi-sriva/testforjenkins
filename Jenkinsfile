//pipeline {
//    agent any
//
//    stages {
//        stage('Build') {
//            steps {
//                sh "./test.sh"
//            }
//        }
//}
//}


node{
    try{
        String environment = 'dev'
        String release_tag= 'latest'
        String service_name= 'molecule'
        String app_name = 'molecule'
        String deployment_name = 'molecule-deployment'
        String container_name = 'molecule'
        String image = 'molecule-build'
        def jenkinsWS = pwd()
        String inputFile=""
        String domainendpoint=""
        String tokenid=""
        Boolean isValid = true
        long deploydate = System.currentTimeMillis();
        Map app
        //stage('PreDeploy'){
        //    Util = load 'infrak8s_repo/Util.groovy'
        //    Util.init(this)
        //    if(environment) {
        //    app = Util.getConfig(service_name, 'infrak8s_repo/config.json')
       // }
       // }
        stage('Deploy'){
            echo ". /etc/profile > /dev/null 2>&1 ; kubectl config use-context devqa"
            tokenid="devtoken"
        }
        echo "def getimagecmd= / kubectl get deployment $deployment_name -o=jsonpath='{$.spec.template.spec.containers[0].image } ' -n $environment /"
        echo "def imagename=sh(script: ". /etc/profile > /dev/null 2>&1 ; ${getimagecmd}", returnStdout: true).trim()"
        echo "def imagetag=imagename.split(":")[1]"
    
        if (release_tag == 'latest'){
            echo "def command = / kubectl patch deployment $deployment_name -p "{\"spec\":{\"template\":{\"metadata\":{\"labels\":{\"date\":\"$deploydate\"}}}}}" -n $environment /"
            echo ". /etc/profile  > /dev/null 2>&1 ; $command"
            echo ". /etc/profile > /dev/null 2>&1 ; kubectl rollout status deployment $deployment_name -n $environment"
        }else{
            echo ". /etc/profile > /dev/null 2>&1 ; kubectl set image deployment $deployment_name $container_name=$image:$release_tag --record -n $environment"
            echo ". /etc/profile > /dev/null 2>&1 ; kubectl rollout status deployment $deployment_name -n $environment"
        }
        stage('post_deploy') {
        }
    }
    catch (Exception e) {
    throw e
    }
return this
}
