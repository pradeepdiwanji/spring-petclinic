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
    stages {
        stage ('Maven container config') {
            stages {
                stage ('Artifactory configuration') {
                    steps {
                        rtMavenDeployer(
                                id: "MAVEN_DEPLOYER",
                                serverId: env.ARTIFACTORY_SERVER_ID,
                                releaseRepo: env.ARTIFACTORY_DEPLOYER_RELEASE_REPO,
                                snapshotRepo: env.ARTIFACTORY_DEPLOYER_SNAPSHOT_REPO
                        )

                        rtMavenResolver(
                                id: "MAVEN_RESOLVER",
                                serverId: env.ARTIFACTORY_SERVER_ID,
                                releaseRepo: env.ARTIFACTORY_RESOLVER_RELEASE_REPO,
                                snapshotRepo: env.ARTIFACTORY_RESOLVER_SNAPSHOT_REPO
                        )
                    }
                }
                stage ('Publish BuildInfo') {
                    steps {
                        rtBuildInfo (
                                captureEnv: true
                        )
                        rtPublishBuildInfo (
                                serverId: env.ARTIFACTORY_SERVER_ID
                        )
                    }
                }
                stage('Build') {
                environment {
                   MAVEN_HOME = '/usr/local/Cellar/maven/3.8.2/libexec'
                   JAVA_HOME= '/Applications/Eclipse JEE.app/Contents/Eclipse/plugins/org.eclipse.justj.openjdk.hotspot.jre.full.macosx.x86_64_16.0.1.v20210528-1205/jre'
                   }
                    steps {
                        rtMavenRun (
                                pom: 'pom.xml',
                                //goals: '-B -DskipTests clean package',
                                goals: 'clean compile install -DskipTests',
                                deployerId: "MAVEN_DEPLOYER",
                                resolverId: "MAVEN_RESOLVER"
                        )
                    }
                }
            }
        }
    }
}