pipeline {
  agent any

  environment {
      ANSIBLE_CONFIG="${WORKSPACE}/ansible.cfg"
    }

    options {
  timestamps ()
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '10', numToKeepStr: '4')
  }

  parameters {
       string(name: 'inventory', defaultValue: 'ci.ini', description: 'selecting the environment')
    }

  stages{
      stage("Initial cleanup") {
          steps {
            dir("${WORKSPACE}") {
              deleteDir()
            }
          }
        }


        stage('Checkout SCM') {
         steps{
            git branch: 'main', changelog: false, credentialsId: 'local-exec', url: 'https://github.com/TheCountt/local-exec.git'
          }
       }


        stage('Prepare Ansible For Execution') {
         steps {
           sh 'echo ${WORKSPACE}' 
           sh 'sed -i "4 a roles_path=${WORKSPACE}/roles" ${WORKSPACE}/ansible.cfg'  
         }
       }

      stage('Execute Ansible playbook') {
        steps {
           ansiblePlaybook colorized: true, credentialsId: 'local-exec', disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory/${inventory}', playbook: 'playbooks/site.yml'
          }
        }

      stage('Clean Workspace after build') {
        steps {
          cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenUnstable: true, deleteDirs: true)
         }
       }



      stage('Trigger another jenkins') {
        steps {
          build job: 'simple-mern-app', propagate: true, wait: true
        }
      }

   }
   
}

