def gradle(command) {
    sh "./gradlew ${command}"
}

node('master') {
	stage('Sync Source Code') {
		checkout scm
	}

	stage('Gradle Build') {
		gradle 'clean assembleDebug check jacocoTestReport'
	}

	stage('Publishing Reports') {
		androidLint canComputeNew: false, 
					defaultEncoding: '', 
					healthy: '', 
					pattern: '**/lint*.xml', 
					unHealthy: ''
		checkstyle 	canComputeNew: false, 
					defaultEncoding: '', 
					healthy: '', 
					pattern: '**/build/reports/checkstyle/checkstyle*.xml', 
					unHealthy: ''
		findbugs 	canComputeNew: false, 
					defaultEncoding: '', 
					excludePattern: '', 
					healthy: '', 
					includePattern: '', 
					pattern: '**/build/reports/findbugs*.xml', 
					unHealthy: ''
		pmd 	canComputeNew: false, 
				defaultEncoding: '', 
				healthy: '', 
				pattern: '**/build/reports/pmd*.xml', 
				unHealthy: ''
		dry 	canComputeNew: false, 
				defaultEncoding: '', 
				healthy: '', 
				pattern: '**/build/reports/cpd*.xml', 
				unHealthy: ''
		jacoco()
	}

	stage('Archive build output') {
		archive '**/*.apk'
	}
}
