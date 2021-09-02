node {
    // Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
            checkout scm
        }
        stage ('Build') {
            environment {
                   MAVEN_HOME = '/usr/local/Cellar/maven/3.8.2/libexec'
                   JAVA_HOME= '/Applications/Eclipse JEE.app/Contents/Eclipse/plugins/org.eclipse.justj.openjdk.hotspot.jre.full.macosx.x86_64_16.0.1.v20210528-1205/jre'
                   }
                        
                        rtMavenRun (
                                pom: 'pom.xml',
                                //goals: '-B -DskipTests clean package',
                                goals: 'clean compile install -DskipTests',
                                deployerId: "MAVEN_DEPLOYER",
                                resolverId: "MAVEN_RESOLVER"
                      
                    }
            
        }
        stage ('Tests') {
            parallel 'static': {
                sh "echo 'shell scripts to run static tests...'"
            },
            'unit': {
                sh "echo 'shell scripts to run unit tests...'"
            },
            'integration': {
                sh "echo 'shell scripts to run integration tests...'"
            }
        }
        stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
        }
       
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}