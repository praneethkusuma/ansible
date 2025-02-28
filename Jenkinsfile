pipeline {
  agent {
      label "built-in"
  }
  options {
    ansiColor('xterm')
  }
  environment {
    ENVIRONMENT = "Prod"
  }
  parameters {
      string(name: 'CODE_BRANCH', defaultValue: 'main', description: 'Code Branch to deploy')
      string(name: 'EXTENSIONS_BRANCH', defaultValue: 'master', description: 'Extensions Branch to deploy')
          }
  stages{
    stage('Ansible Run') {
      steps {
        script {
          if(env.wild1 == "true" ){
            sh "cd ${WORKSPACE}/${ENVIRONMENT} && ansible-playbook playbook.yml  -i inventory  --extra-vars 'host_group=wild1 code_branch=${CODE_BRANCH} extensions_branch=${EXTENSIONS_BRANCH}'"
          }
           else {
               if(env.wild2 == 'true'){
                sh "cd ${WORKSPACE}/${ENVIRONMENT} && ansible-playbook playbook.yml  -i inventory  --extra-vars 'host_group=wild2 code_branch=${CODE_BRANCH} extensions_branch=${EXTENSIONS_BRANCH}'"
               }
           }   
        }
      }
    }
  }
}
