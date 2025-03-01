pipeline {
  agent {
      label "built-in"
  }
  environment {
        ENVIRONMENT = "Prod"
  }
  parameters {
        string(name: 'CODE_BRANCH', defaultValue: 'main', description: 'Code Branch to deploy')
        string(name: 'EXTENSIONS_BRANCH', defaultValue: 'master', description: 'Extensions Branch to deploy')
            }
  stages{
        stage('Begin Notifier') {
            steps {
                script {
                    echo "Ansible started "
                }
            }
        }
        stage('Ansible Run') {
            steps {
                script {
                def environments = ['wild1', 'wild2']
                def selectedEnvironments = environments.findAll { envName -> env."${envName}" == "true" }
                if (selectedEnvironments) {
                    sh """
                        ansible-playbook playbook.yml -i inventory --extra-vars 'host_group=${selectedEnvironments.join(",")} code_branch=${CODE_BRANCH} extensions_branch=${EXTENSIONS_BRANCH}'
                    """
                   }
                }
            }
        }
    }
}



            // script {
            //     def environments = ['wild1', 'wild2']
            //     environments.each { envName ->
            //         if (env."${envName}" == "true") {
            //             sh """
            //                 ansible-playbook playbook.yml -i ${envName}/inventory --extra-vars 'code_branch=${CODE_BRANCH} extensions_branch=${EXTENSIONS_BRANCH}'
            //             """
            //         }
            //     }
            // }