pipeline 
{
	agent any
	stages 
	{    
		stage('4.Uploading Databag') 
		{
			steps 
			{
				bat '''
					cd /d C:\\Program Files\\PuTTY
					putty -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\upload_databag.txt llg00fic.uk.oracle.com
				'''
				bat 'echo "Step 4"'                
			}
		}
		stage('5.Vault Installation') 
		{
			steps 
			{
				bat 'echo "Step 5"'
			}
		}        
		stage('6.OCMS Prerequisites') 
		{
			steps 
			{
				bat 'echo "Step 6"'
			}
		}
		stage('7.DB Installation') 
		{
			steps 
			{
				bat 'echo "Step 7"'
			}
		}
		stage('8.MI Domain Creation') 
		{
			steps 
			{		
				bat 'echo "Step 8"'
			}
		}
		stage('9.Starting Servers') 
		{
			steps 
			{
				bat 'echo "Step 9"'
			}
		}
		stage('10.OCMS Deployments') 
		{
			steps 
			{
				bat 'echo "Step 10"'
			}
		}
		stage('11.Restarting All Servers') 
		{
			steps
			{
				bat 'echo "Step 11"'
			}
		}        
	}
	post 
	{
		always 
		{
			winRMClient credentialsId: 'OCMS_CREDENTIALS', hostName: 'OCMS_HOSTNAME', winRMOperations: [invokeCommand('mkdir C:\\Monal')]
		}
		success 
		{
			echo 'This will run only if successful'
		}
		failure 
		{
			echo 'This will run only if failed'
		}
		unstable 
		{
			echo 'This will run only if the run was marked as unstable'
		}
		changed 
		{
			echo 'This will run only if the state of the Pipeline has changed'
			echo 'For example, if the Pipeline was previously failing but is now successful'
		}
	}
}
