def dockerImage = 'docker.custenborder.com/jcustenborder/drunken-octopus-marlin:0.0.9'
def docsRepository = 'git@github.com:drunken-octopus/drunken-octopus.github.io.git'
node {
    deleteDir()
    checkout scm

    stage('build') {
        withDockerRegistry(credentialsId: 'custenborder_docker', url: 'https://docker.custenborder.com') {
            docker.image(dockerImage).inside {
                sh 'mkdocs build'
                archiveArtifacts "site/**/*"
            }
        }
    }

    if (env.BRANCH_NAME == 'docs') {
        stage('publish') {
            sh 'mkdir build'
            dir('build') {
                git branch: 'master', changelog: false, credentialsId: 'jenkins-drunkenoctop.us', poll: false, url: docsRepository 
                sh 'rsync --exclude ".git" -avz --delete ../site/* .'
                sh 'git config user.email "jenkins+drunken-octopus@custenborder.com"'
                sh 'git config user.name "Jenkins"'
                sh "echo `git add --all . && git commit -m 'Build ${BUILD_NUMBER}' .`"
                sshagent(credentials: ['jenkins-drunkenoctop.us']) {
                    sh "git push '${docsRepository}' gh-pages"
                }
            }
        }
    }
}
