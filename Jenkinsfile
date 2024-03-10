node{
    def mavenHome = tool name 'maven 3.9.6'
    stage('1clonecode'){
        git 'https://github.com/Geofrey498/liontech-online-library-web-app.git'


    }

    stage('2Test&Buildapp'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('3CodeQuality'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('4UploadArtifacts'){
        sh "${mavenHome}/bin/mvn deploy"

    }
    



}