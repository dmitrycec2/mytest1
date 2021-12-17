def BRANCH_NAME = 'main'
pipeline {
  parameters { // {
    string(
      name: 'P_GIT_BRANCH',
      description: '',
      defaultValue: 'main'
    )

    choice(
      name: 'P_SLAVE1',
      description: '',
      choices: ['NULL', 'UC_251_NEWFILE_run'] as List
    )
    choice(
      name: 'P_ENCODING',
      description: '',
      choices: ['utf8'] as List
    )
  } // }
  agent none
  options {
    skipDefaultCheckout()
    buildDiscarder(logRotator(
      numToKeepStr: '10' + (BRANCH_NAME == 'dev' ? '' : '0'),
      daysToKeepStr: '10' + (BRANCH_NAME == 'dev' ? '' : '0'),
    ))
  }
  stages {
    stage('Test') {
	  agent {
    label 'slave1'
  }
	          steps {
            script {
              scmInfo = checkout scm
			  f = fileExists 'README.md'
			  echo "f=${f}"
			  sh 'chmod +x test.sh'
			  sh 'chmod +x run.sh'
			  sh 'chmod +x build.sh'
			  sh 'chmod +x entrypoint.sh'
			  sh './test.sh ${P_TEST_MODE}'
            }
          }
	}
	}
 
}
