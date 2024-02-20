def application =params.Application
def action =params.Action
def datacenter =params.DC


pipeline {
    agent any

    stages {

        stage('Pull server details') {
            steps{
				println "dc from job parameter : " + datacenter   
                println "action from job parameter: " + action
                println "application from job parameter " + application
				git branch: 'main', poll: false, url: 'https://github.com/Mamtagupta2503/publicrepo.git'

            }
        }
		stage('Parallel execution') {
			parallel {
				stage('serviceability') {
					when {
						expression {
						'serviceability' in application||'ALL' in application
						}
					}
					steps {
						script{
							try {
								println "Performing "+ action +" on application serviceability"								
								def serverdetails = readJSON file: 'serviceability.json'
								def haproxyservers = serverdetails.HAPROXY_SERVERS 
								def nceserver = serverdetails.HA_NCE_SERVERS
								def ncwserver = serverdetails.HA_NCW_SERVERS
								def backend = serverdetails.BACKEND
								def sockfileloc = serverdetails.SOCKFILE
								def server

								if(datacenter =='NCE'){
									 server = nceserver
									 println "NCE server are: " + server
								}
								else if(datacenter =='NCW'){
									server = ncwserver
									println "NCW server are: " + server
								}
								for(ha in haproxyservers) {
									def SSH_OPTION="ssh jenkins_worker@${ha} -o StrictHostKeyChecking=no"
									for(bknd in backend) {
										for(s in server) {
											echo "$action server: ${s} on haproxy: ${ha} backend ${bknd}"
											//sh "$SSH_OPTION 'echo $action server $bknd/$s | sudo socat stdio $sockfileloc'"
										}
									}
								}			
							}catch(Exception e) {
								catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
								sh "exit 1"
								}
							}
						}
					}      
				}
				stage('Smartsheet') {
					when {
						expression {
						'Smartsheet' in application||'ALL' in application
						}
					}
				steps {
					script{
						try {
							println "Performing "+ action +" on application serviceability"	
							def serverdetails = readJSON file: 'smartsheet.json'
							def haproxyservers = serverdetails.HAPROXY_SERVERS 
							def nceserver = serverdetails.NCESERVERS
							def ncwserver = serverdetails.NCWSERVERS
							def backend = serverdetails.BACKEND
							def sockfileloc = serverdetails.SOCKFILE
							def server

							if(datacenter =='NCE'){
								server = nceserver
								println "NCE server are: " + server
							}
							else if(datacenter =='NCW'){
								server = ncwserver
								println "NCW server are: " + server

							}

							for(ha in haproxyservers) {
								def SSH_OPTION="ssh jenkins_worker@${ha} -o StrictHostKeyChecking=no"
								for(bknd in backend) {
									for(s in server) {
									echo "$action server: ${s} on haproxy: ${ha} backend ${bknd}"
								   //sh "$SSH_OPTION 'echo $action server $bknd/$s | sudo socat stdio $sockfileloc'"						
								   }
								}
							}
						}catch(Exception e) {
							result = 'failed'
							catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
								sh "exit 1"
							}
						}
					}      
				}
			}
				stage('PaymentUI') {
					when {
						expression {
						'PaymentUI' in application||'ALL' in application
						}
					}
				steps{
					script{
						try {
						println "Performing "+ action +" on application PaymentUI"
						def serverdetails = readJSON file: 'payment-ui.json'
						def haproxyservers = serverdetails.HAPROXY_SERVERS 
						def nceserver = serverdetails.NCESERVERS
						def ncwserver = serverdetails.NCWSERVERS
						def backend = serverdetails.BACKEND
						def sockfileloc = serverdetails.SOCKFILE
						def server

						if(datacenter =='NCE'){
							server = nceserver
							println "NCE server are: " + server
						}
						else if(datacenter =='NCW'){
							server = ncwserver
							println "NCW server are: " + server
						}

						for(ha in haproxyservers) {
							def SSH_OPTION="ssh jenkins_worker@${ha} -o StrictHostKeyChecking=no"
							for(bknd in backend) {
								for(s in server) {
									echo "$ACTION server: ${s} on haproxy: ${ha} backend ${bknd}"
									//sh "$SSH_OPTION 'echo $action server $bknd/$s | sudo socat stdio $sockfileloc'"
							   }
							}
						}
						}catch(Exception e) {
							catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
								sh "exit 1"
							}
						}
					}    
				}
			}
				stage('OOBServiceRouter') {
					when {
					expression {
					'OOBServiceRouter' in application||'ALL' in application

					}
					}
				steps {
					script{
						println "Performing "+ action +" on application OOBServiceRouter"
						try {  
						def serverdetails = readJSON file: 'OOBServiceRouter.json'
						def haproxyservers = serverdetails.HAPROXY_SERVERS 
						def nceserver = serverdetails.NCESERVERS
						def ncwserver = serverdetails.NCWSERVERS
						def backend = serverdetails.BACKEND
						def sockfileloc = serverdetails.SOCKFILE
						def server

						if(datacenter =='NCE'){
							server = nceserver
							println "NCE server are: " + server
						}
						else if(datacenter =='NCW'){
							server = ncwserver
							println "NCW server are: " + server
						}

						for(ha in haproxyservers) {
							def SSH_OPTION="ssh jenkins_worker@${ha} -o StrictHostKeyChecking=no"
							for(bknd in backend) {
								for(s in server) {
									echo "$action server: ${s} on haproxy: ${ha} backend ${bknd}"
									//sh "$SSH_OPTION 'echo $action server $bknd/$s | sudo socat stdio $sockfileloc'"
								}
							}
						}
						}catch(Exception e) {
							catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
								sh "exit 1"
							}
						}
					}
				}      
			}
				stage('MTG Pub-UI') {
					when {
					expression {
					'MTG Pub-UI' in application||'ALL' in application

					}
					}
				steps {
					script{
						try {  
						println "Performing "+ action +" on application MTG Pub-UI/mobiletokenui"
						def serverdetails = readJSON file: 'mobiletokenui.json'
						def haproxyservers = serverdetails.HAPROXY_SERVERS 
						def nceserver = serverdetails.NCESERVERS
						def ncwserver = serverdetails.NCWSERVERS
						def backend = serverdetails.BACKEND
						def sockfileloc = serverdetails.SOCKFILE
						def server

						if(datacenter =='NCE'){
							server = nceserver
							println "NCE server are: " + server
						}
						else if(datacenter =='NCW'){
							server = ncwserver
							println "NCW server are: " + server
						}

						for(ha in haproxyservers) {
							def SSH_OPTION="ssh jenkins_worker@${ha} -o StrictHostKeyChecking=no"
							for(bknd in backend) {
								for(s in server) {
									echo "$ACTION server: ${s} on haproxy: ${ha} backend ${bknd}"
									//sh "$SSH_OPTION 'echo $action server $bknd/$s | sudo socat stdio $sockfileloc'"
								}
							}
								
						}
						}catch(Exception e) {
							catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
								sh "exit 1"
							}
						}
					}
				}      
			}
			} 
		}	 
    }   
}
