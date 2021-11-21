#!groovy


pipeline {
	agent none
	
	parameters {
		string(name: 'ZOSMF_RELEASE', defaultValue: 'HSMA257', description: 'z/OSMF Release name, a.k.a. FMID.')
		string(name: 'APAR_NAME', defaultValue: '', description: 'The APAR Name like PH12345')
		choice(name: 'POPULATE_FLAG', choices: ['NO','YES'], description: 'If you want to populate the build artifacts for functional test.')
		choice(name: 'PACKAGE_FLAG', choices: ['NO','YES'], description: 'If you want an ++USERMOD/++APAR/++PTF packaged.')
		choice(name: 'BUILD_TYPE', choices: ['usermod','apar','ptf'], description: 'The type of fix you are packaging.')
		string(name: 'ZOSMF_BASE_DRIVER', defaultValue: 'COPYSENT', description: 'z/OSMF base Driver name on which the USERMOD/APAR driver will be based.')
		choice(name: 'DELTA_BUILD_FLAG', choices: ['YES','NO'], description: 'If you want a delta build.')
		string(name: 'TRANS_NODE_ID', defaultValue: 'S390VM.SRVLIB-PLPSC.CBUILD', description: 'APARs or PTFs will be send to SRVLIB and CBUILD by default.')
		choice(name: 'OVERRIDE_RELATIONSHIP_CHECK', choices: ['NO','YES'], description: 'If you want to bypass validation that checks manual relationships. It is recommended that this variable always be set to NO unless it explicitly needs to be set to YES for a single run. If this is set incorrectly/unintentionally it could potentially lead to a PE as critical checks are being bypassed. So please only use this when absolutely needed!')
		choice(name: 'PACKAGE_DIRECTLY', choices: ['NO','YES'], description: 'If you want to package USERMOD/APAR/PTF directly. It is recommended that this variable always be set to NO unless it explicitly needs to be set to YES for a single run. If this value is set to YES, the "Invoke zService Package" stage will be performed directly.')
		choice(name: 'ALLOW_FEWER_PARTS', choices: ['NO','YES'], description: 'If you want to remove some parts from an APAR/PTF. It is recommended that this variable always be set to NO unless it explicitly needs to be set to YES for a single run. If this is set incorrectly/unintentionally it could potentially lead to a PE as critical checks are being bypassed. So please only use this when absolutely needed!')
		choice(name: 'ZPACKAGE_SERVER_PORT', choices: ['8311','8321'], description: 'The port number of zPackageServer(Please try to switch to another port, when the other one is down).')
	}
	
	options {
		// Skip checking out code from source control by default in the agent directive
		skipDefaultCheckout()
		// Disallow concurrent executions of the Pipeline 
		disableConcurrentBuilds()
		// only keep 15 builds to prevent disk usage from growing out of control
		buildDiscarder(
			logRotator(
				daysToKeepStr: '15',
				numToKeepStr: '15',
			)
		)
	}
	
	stages {
	
		stage('Build z/OSMF Workflow from zmf_workflow') {
		
			agent any

			steps {
			
				echo "build"
			}
		}
		
		stage('Create DISTLIBS') {
			
			agent any

			steps {
				echo "create"
			}
		}
	}
	
	post {
		failure {
			echo 'ZMF_WORKFLOW CI BUILD PIPELINE FAILED.'
		}
		success {
			echo 'ZMF_WORKFLOW CI BUILD PIPELINE SUCCESSFUL.'
		}
		unstable {
			echo 'ZMF_WORKFLOW CI BUILD PIPELINE UNSTABLE.'
		}
	}
}
