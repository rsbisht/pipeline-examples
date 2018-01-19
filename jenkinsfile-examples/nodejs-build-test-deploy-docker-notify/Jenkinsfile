#!groovy

node('Server_Group_1') {

    currentBuild.result = "SUCCESS"

    try {

            stage('Checkout'){

            env.NODE_ENV = "Checkout"

            print "[Stage] : ${env.NODE_ENV}"

            sh "echo                                                       > ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"

	    checkout scm

       }

       stage('Test'){

            env.NODE_ENV = "Test"

            print "[Stage] : ${env.NODE_ENV}"

	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"

	    sh "ls -lrt ${WORKSPACE}                                      >> ${env.JOB_NAME}.log"

       }

       stage('Build'){

            env.NODE_ENV = "Build"

            print "[Stage] : ${env.NODE_ENV}"

	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"

	    sh "echo Building the code..                                  >> ${env.JOB_NAME}.log"

            // sh 'export MAVEN_HOME=/opt/maven; cd ${WORKSPACE}; ${MAVEN_HOME}/bin/mvn clean install'

	    sh "javac SimpleForLoop.java"
	    sh "java SimpleForLoop                                        >> ${env.JOB_NAME}.log"

       }

       stage('Deploy'){

            env.NODE_ENV = "Deploy"

            print "[Stage] : ${env.NODE_ENV}"

	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"
	    sh "Copy the Jenkinsfile to Deployment server....             >> ${env.JOB_NAME}.log"

	    sh 'rsync ${env.WORKARERA}/Jenkinsfile root@15.213.52.106:/tmp'

       }

       stage('Cleanup'){

            env.NODE_ENV = "Deploy"

            print "[Stage] : ${env.NODE_ENV}"

	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"
	    sh "Cleaning up the files....                                 >> ${env.JOB_NAME}.log"

	    mail    from: 'rsbisht@hpe.com',
                 replyTo: 'rsbisht@hpe.com',
                      to: 'rsbisht@hpe.com',
                 subject: 'Project Build Successful',
	            body: 'Project Build Successful' 
       }

    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail    from: 'rsbisht@hpe.com',
                 replyTo: 'rsbisht@hpe.com',
                      to: 'rsbisht@hpe.com',
                 subject: 'Project Build Failed !',
	            body: "Project Build Failed ! You can find the error is here: ${env.BUILD_URL}" 

        throw err
    }

}
