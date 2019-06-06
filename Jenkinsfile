node{

	properties([
		parameters([
			text(name: "GIT_BRANCH", defaultValue:'master',description:"Git branch to pull"),
			text(name: "MAVEN_OPTIONS", defaultValue:'-Dmaven.test.failure.ignore=true',description:"maven options")
		])
	])
	
	stage('Start'){
		echo 'starting basic SOA application deployment' 
	}

	stage('Checkout'){
		echo 'git retrieve application from distant repo'
		checkout scm
		bat "git -eXU checkout ${params.GIT_BRANCH}"
	}

	stage('Package'){
		echo 'maven clean package'
		// va lire dans le fichier settings.xml de Maven (binaire installé/utilisé, repertoire conf)
		// le nom fileid importe peu, c'est un identifiant local
		//configFileProvider(
       	// 	[configFile(fileId: 'maven-settings', variable: 'MAVEN_SETTINGS')]) {
		
				bat "mvn clean package -eXU ${params.MAVEN_OPTIONS}"
		//}
	}

	stage('pre-integration'){
		echo 'maven pre-integration-test'
		//configFileProvider([
		//	configFile(fileId='settings.xml', variable='MAVEN_SETTINGS')]){
				bat "mvn pre-integration-test -eUX ${params.MAVEN_OPTIONS}"
		//	}
	}
	
	stage('deploy'){
		echo 'maven deploy to local env'
		//configFileProvider([
		//	configFile(fileId='settings.xml', variable='MAVEN_SETTINGS')]){
				bat "mvn deploy -eXU ${params.MAVEN_OPTIONS}"
		//	}
		
	}




}