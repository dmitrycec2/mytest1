def BRANCH_NAME = 'main'
pipeline {
  parameters { // {
    string(
      name: 'P_DOCKER_TAG',
      description: '',
      defaultValue: 'feature_dev'
    )
    string(
      name: 'P_PORT',
      description: 'порт',
      defaultValue: '80'
    )
    string(
      name: 'P_HOST',
      description: 'хост',
      defaultValue: 'dev.planeta.ibs'
    )
    string(
      name: 'P_SCHEME',
      description: 'протокол',
      defaultValue: 'http'
    )
    string(
      name: 'P_DURATION',
      description: 'продолжительность теста, секунды',
      defaultValue: '600'
    )
    string(
      name: 'P_THREADGROUP',
      description: 'количество пользователей',
      defaultValue: '1'
    )
    string(
      name: 'P_RAMPUPPERIOD',
      description: 'время выхода пользователей',
      defaultValue: '1'
    )
    string(
      name: 'P_LOOPCOUNT',
      description: 'количество повторов',
      defaultValue: '-1'
    )
    string(
      name: 'P_IS_PACINGON',
      description: 'Включить ожидание пользователей после выполнения скрипта',
      defaultValue: 'выключить'
    )
    choice(
      name: 'P_TEST_MODE',
      description: '',
      choices: ['UC_251_NEWFILE_run', 'UC_251_NEWFILE_run'] as List
    )
    choice(
      name: 'P_ENCODING',
      description: '',
      choices: ['utf8'] as List
    )
  } // }
  agent {
    label 'slave1'
  }
  options {
    skipDefaultCheckout()
    buildDiscarder(logRotator(
      numToKeepStr: '10' + (BRANCH_NAME == 'dev' ? '' : '0'),
      daysToKeepStr: '10' + (BRANCH_NAME == 'dev' ? '' : '0'),
    ))
  }
  stages {
    stage('Build') {
	          steps {
            script {
              scmInfo = checkout scm
			  f = fileExists 'README.md'
			  echo "f=${f}"
			  sh 'chmod +x test.sh'
			  sh 'chmod +x run.sh'
			  sh 'chmod +x build.sh'
			  sh 'chmod +x entrypoint.sh'
			  sh "./test.sh '${P_TEST_MODE}'
            }
          }
	}
	}
 
}
