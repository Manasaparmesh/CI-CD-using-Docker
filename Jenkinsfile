pipeline 
{
    agent any
	
	  tools
    {
       maven "Maven"
    }
stages 
{
	stage('checkout') 
	{
        	steps 
		{
             
                	git branch: 'master', url: 'https://github.com/Manasaparmesh/CI-CD-using-Docker.git'
             
          	}
        }
	stage('Execute Maven') 
	{
		steps 
		{
			sh 'mvn package'             
         	 }
        }
        

  	stage('Docker Build and Tag') 
	 {
           steps 
		 {
			 sh 'docker build -t samplewebapp:latest .' 
               		 sh 'docker tag samplewebapp manasaparmesh/samplewebapp:latest'
                             
          	}
        }
     
	 stage('Publish image to Docker Hub') 
	 {
		 steps 
		 {
       			 withDockerRegistry([ credentialsId: "", url: ""  ]) 
			 {
        			 sh  'docker push manasaparmesh/samplewebapp:latest'
         			// sh  'docker push manasaparmesh/samplewebapp:$BUILD_NUMBER' 
     			  }
                
        	 }
    	  }
     
      stage('Run Docker container on Jenkins Agent') 
	{
             
            steps 
		{
                	sh "docker run -d -p 8005:8080 manasaparmesh/samplewebapp"
 	
            	}
        }
	stage('Run Docker container on remote hosts') 
	{
		steps 
		{
			sh "docker -H ssh://ubuntu@172.31.26.106 run -d -p 8005:8080 manasaparmesh/samplewebapp"
          	 }
        }
    }
}

    
