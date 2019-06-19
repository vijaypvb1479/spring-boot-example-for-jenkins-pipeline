def version = "${env.BUILD_NUMBER}"
def GIT_COMMIT_SHORT = null
def GIT_COMMIT = null
def GIT_URL = null
def GIT_BRANCH = null
def BUILD_DATE = null


//def DEPLOYMENT_PROJECTS = [new DeploymentProject(name: 'bff-mobile-trade', path: 'bff', integrationTestRequired: false,
//                imageStreamName: 'bff-mobile-trade-v1', openshiftDeployRequired: false)]

node() {
    stage('Checkout Source') {
       def scmVars = checkout scm
       echo "Checkedout ${scmVars} deployment projects are " //${DEPLOYMENT_PROJECTS}"
       GIT_COMMIT_SHORT = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
       BUILD_DATE = sh(returnStdout: true, script: ' date +%Y-%m-%d-%H-%M-%S').trim()
        
       GIT_COMMIT = scmVars.GIT_COMMIT
       GIT_URL = scmVars.GIT_URL
       GIT_BRANCH = scmVars.GIT_BRANCH
        echo "${GIT_COMMIT_SHORT} - ${BUILD_DATE} - ${GIT_COMMIT} - ${GIT_URL} - ${GIT_BRANCH} - ${version} - ${BUILD_ID}"
    }
    
    stage('Build'){
        sh "./gradlew -Pversion=${version} build"
         step([$class: 'JUnitResultArchiver', testResults: '*/test-results/*.xml'])
    }
    
   
}
