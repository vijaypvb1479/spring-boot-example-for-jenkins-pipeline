def version = "${env.BUILD_NUMBER}"
def GIT_COMMIT_SHORT = null
def GIT_COMMIT = null
def GIT_URL = null
def GIT_BRANCH = null
def BUILD_DATE = null

node() {
    stage('Checkout Source') {
       def scmVars = checkout scm
       echo "Checkedout ${scmVars} deployment projects are ${DEPLOYMENT_PROJECTS}"
       GIT_COMMIT_SHORT = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
       BUILD_DATE = sh(returnStdout: true, script: ' date --utc -Iseconds').trim()
       GIT_COMMIT = scmVars.GIT_COMMIT
       GIT_URL = scmVars.GIT_URL
       GIT_BRANCH = scmVars.GIT_BRANCH
        echo "${GIT_COMMIT_SHORT} - ${BUILD_DATE} - ${GIT_COMMIT} - ${GIT_URL} - ${GIT_BRANCH} - ${version} - ${BUILD_ID}"
    }
}
