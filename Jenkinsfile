pipeline {
    agent any
    
    tools {
             maven 'maven'
             jdk 'java'
        }
        
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'master', credentialsId: 'github-credentials', url: 'https://github.com/SaiBadri/Sample_Login_App.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('ssh to GCP VM') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'tomcat-server01', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/', remoteDirectorySDF: false, removePrefix: '/target', sourceFiles: '**/*.jar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }








    }
}














// pipeline {
//     agent any

//     tools {
//          maven 'maven'
//          jdk 'java'
//     }

//     environment {
//         REPO_URL = 'https://github.com/SaiBadri/java-hello-world-with-maven.git'
//         BRANCH = 'sample-dev'
//         GCP_VM = '35.244.31.178'
//         SSH_USER = 'badri'
//         SSH_KEY = '/Users/badri/.ssh/id_rsa'
//         JAR_FILE = '/Users/badri/Documents/GitHub_Projects/java-hello-world-with-maven/target'
//         DEPLOY_PATH = '/opt/tomcat/apache-tomcat-10.1.24/webapps'
//     }

//     stages {
//         stage('Checkout Code') {
//             steps {
//                 script {
//                     // Checkout the code from the feature branch
//                     git branch: "${BRANCH}", url: "${REPO_URL}"
//                 }
//             }
//         }

//         stage('Build JAR') {
//             steps {
//                 sh 'mvn clean package'
//             }
//         }

//         // stage('Push JAR to GitHub') {
//         //     steps {
//         //         script {
//         //             // Commit and push the JAR file to the GitHub repository
//         //             sh """
//         //                 git add ${JAR_FILE}
//         //                 git commit -m 'Add JAR file'
//         //                 git push origin ${BRANCH}
//         //             """
//         //         }
//         //     }
//         // }

//         stage('Deploy to GCP VM') {
//             steps {
//                 script {
//                     // Copy the JAR file to the GCP VM using SCP
//                     sh """
//                         scp -i ${SSH_KEY} ${JAR_FILE} ${SSH_USER}@${GCP_VM}:${DEPLOY_PATH}
//                     """
                    
//                     // Restart the Tomcat server on the GCP VM
//                     sshagent(['your-ssh-credentials-id']) {
//                         sh """
//                             ssh -o StrictHostKeyChecking=no -i ${SSH_KEY} ${SSH_USER}@${GCP_VM} << EOF
//                                 sudo systemctl restart tomcat
//                                 exit
//                             EOF
//                         """
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Deployment successful!'
//         }
//         failure {
//             echo 'Deployment failed!'
//         }
//     }
// }