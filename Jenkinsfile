pipeline {
    agent any
    environment {
        CRED_ID = 'admin_pradeep_artifactory'
        ARTIFACTORY_SERVER_ID = 'localhost'
        ARTIFACTORY_DEPLOYER_RELEASE_REPO = 'local-repo-maven'
        ARTIFACTORY_DEPLOYER_SNAPSHOT_REPO = 'local-repo-maven'
        ARTIFACTORY_RESOLVER_RELEASE_REPO = 'local-repo-maven'
        ARTIFACTORY_RESOLVER_SNAPSHOT_REPO = 'local-repo-maven'
    }
    
    stage ('Clone') {
            checkout scm
        }
        
}