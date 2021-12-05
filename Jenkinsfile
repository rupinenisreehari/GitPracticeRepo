node('jdk11-mvn3.8.4') {
    properties([parameters([choice(choices: ['scripted', 'master', 'declarative'], description: 'branch to be built', name: 'BRANCH_TO_BUILD')])])
    stage('git') {
        git url: 'https://github.com/GitPracticeRepo/java11-examples.git', branch: "${params.BRANCH_TO_BUILD}"
    }
    stage('build') {
        sh '''
            echo "PATH=${PATH}"
            echo "M2_HOME=${M2_HOME}"

        '''
        sh '/usr/local/apache-maven-3.8.4/bin/mvn clean package'
    }
    stage('archive') {
        archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
    }
    stage('publish test reports') {
        junit '**/TEST-*.xml'
    }
}