def ID
node {
	
	stage('checkout'){

         	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/pocandroid/devops-ios.git']]])

	    }
	
      	stage('Build'){
          	sh label: '', script: '''#!/bin/bash
         	appcenter login --token acecc33a1795c0b581442a4f93503b1338586c65
         	appcenter build queue -b master --app devopsmobility/sample-ios
         	sleep 130
		ID=$(appcenter build branches show -b master --app devopsmobility/sample-ios | grep ID: |cut -f 2 -d ":")
        	appcenter build download --app devopsmobility/sample-ios -t build --id ${ID} --file Sample_iOS
         	'''
	    }
        stage('Nexus Repository'){	

	    nexusArtifactUploader artifacts: [[artifactId: 'sample_iOS', classifier: '', file: '/var/lib/jenkins/workspace/Newios/Sample_iOS.ipa', type: 'ipa']], credentialsId: 'bcebae3d-4df0-4fb2-8ca4-6ee8af37cabb', groupId: 'com.ios.devops', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'devopsmobility', version: '7.0'

	}    
 }
