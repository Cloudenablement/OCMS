pipeline 
{
	agent any
	stages 
	{    
		stage('4.Uploading Databag') 
		{
			steps 
			{
				bat 'echo "Step 4"' 
				bat '''
					cd /d C:\\Program Files\\PuTTY
					echo y|plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\upload_databag.txt llg00fic.uk.oracle.com
				'''								
			}
		}
		stage('5.Vault Installation') 
		{
			steps 
			{				
				bat 'echo "Step 5"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\install_vault.txt llg00fic.uk.oracle.com
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'"
				'''								
			}
		}        
		stage('6.OCMS Prerequisites') 
		{
			steps 
			{
				bat 'echo "Step 6"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\ocms_prerequisites.txt llg00fic.uk.oracle.com
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'"
				'''								
			}
		}
		stage('7.DB Installation') 
		{
			steps 
			{
				bat 'echo "Step 7"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\install_db.txt llg00fic.uk.oracle.com
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'"
				'''								
			}
		}
		stage('8.MI Domain Creation') 
		{
			steps 
			{		
				bat 'echo "Step 8"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\install_mi.txt llg00fic.uk.oracle.com
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'"
				'''								
			}
		}
		stage('9.Starting Servers') 
		{
			steps 
			{
				bat 'echo "Step 9"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\start_admin.txt llg00fic.uk.oracle.com
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'"
				'''								
			}
		}
		stage('10.OCMS Deployments') 
		{
			steps 
			{
				bat 'echo "Step 10"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\install_ocms.txt llg00fic.uk.oracle.com
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'"
				'''								
			}
		}
		stage('11.Restarting All Servers') 
		{
			steps
			{
				bat 'echo "Step 11"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\start_all_servers.txt llg00fic.uk.oracle.com
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'"
				'''								
			}
		}        
	}
	post 
	{
		always 
		{
			echo 'This will always run'
			bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\Revertchange.txt llg00fic.uk.oracle.com					
			'''
			mail 	to: 'ravi.al.oracle.com',
             		     	subject: "Pipeline: ${currentBuild.fullDisplayName}",
             			body: "Build URL ${env.BUILD_URL}"
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
