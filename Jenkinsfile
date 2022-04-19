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
       string(name: 'tags', defaultValue: 'Specify the tag to limit the ansible execution')
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
            git branch: 'master', credentialsId: 'bitbucket', url: 'https://TheCountt@bitbucket.org/anpbucket/anpbucket-ci-cd.git'
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
           ansiblePlaybook become: true, becomeUser: 'jenkins', colorized: true, credentialsId: 'private-ssh-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory/${inventory}', playbook: 'playbooks/site.yml'
          }
        }

      stage('Clean Workspace after build'){
        steps{
          cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenUnstable: true, deleteDirs: true)
         }
       }
   }
}

