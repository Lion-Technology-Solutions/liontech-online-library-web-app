node{
    def mavenHome = tool name: 'maven 3.9.6'
    stage('1clonecode'){
        git 'https://github.com/Geofrey498/liontech-online-library-web-app.git'
    }
    stage('2Test&Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('3CodeQuality'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('4UploadArtifacts'){
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('5deploy2DevEnv'){
        sh "echo 'deploying to dev  environment"
        deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://3.99.154.176:8009/')], contextPath: 'dev ', war: 'target/*.war'
    }
    stage('6DeploytoTestENV'){
        sh "echo 'deploy to test Environment' "
        deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://3.99.154.176:8009/')], contextPath: 'test', war: 'target/*.war'
    }
    stage('7Deploy2UAT'){
        sh "echo 'deploy to UAT or staging Environment' "
        deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://3.99.154.176:8009/')], contextPath: 'staging', war: 'target/*.war'
    }
    stage('8Approval&review+prep4prod'){
        sh "echo  'application is ready for review and prod release' "
        timeout(time:5 unit: 'DAYS'){
        input message: "App is ready for release to prod, please review and signup"    
        }
    }

    stage('9DEPLOY2PROD'){
        sh "sleep 50"
        deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://3.99.154.176:8009/')], contextPath: 'production', war: 'target/*.war'
    }
    stage('congratulationsforrelease'){
        echo 'congratulations for online library prod release'

    }
    stage('sendMS Team Notifications'){
        office365ConnectorSend color: 'blue', message: 'practice reaps', status: 'done', webhookUrl: 'https://liontechacademy.webhook.office.com/webhookb2/846e2690-7cbd-4336-a761-133302212d6d@b290c85e-0692-4ada-8f25-2a3b60aca73e/JenkinsCI/c29f5083703c4a3e9f5840c625064ea0/5bfbc321-9730-49f4-87d1-ed42fa9aacde'
    }












}