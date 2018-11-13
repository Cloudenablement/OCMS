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
				mail to: 'ravi.al.kumar@oracle.com,monal.kumar@oracle.com',
             				  subject: "OCMS Installation Status",
             				  body: "Uploading Databag SUCCESS\n\nProgress: (5% Completed)\n\n\n\n\n\nRegards,\nCloud Enablement Team"				
				bat 'echo "Step 5"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\OCMS_files\\install_vault.txt llg00fic.uk.oracle.com					
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'" -param1 'Vault Installation' -param2 'Progress: (10% Completed)'  
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
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'" -param1 'OCMS Prerequisites' -param2 'Progress: (30% Completed)' 
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
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'" -param1 'DB Installation' -param2 'Progress: (50% Completed)' 
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
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'" -param1 'MI Domain Creation' -param2 'Progress: (70% Completed)' 
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
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'" -param1 'Starting Servers' -param2 'Progress: (80% Completed)' 
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
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'" -param1 'OCMS Deployments' -param2 'Progress: (90% Completed)' 
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
					powershell.exe -NonInteractive -ExecutionPolicy Bypass "& 'C:\\run_chef_client.ps1'" -param1 'Restarting All Servers' -param2 'Progress: (100% Completed)' 
				'''								
			}
		}        
	}
	post 
	{		
		success 
		{
			echo 'OCMS INSTALLATION COMPLETED SUCCESSFULLY'
			mail to: 'ravi.al.kumar@oracle.com,monal.kumar@oracle.com',
             		     subject: "OCMS Installation Completed",
             		     body: "Overall OCMS Setup Done Successfully.\n\nOCMS Server is ready now.\n\n\n\n\n\nRegards,\nCloud Enablement Team"								
		}
		failure 
		{					
			echo 'OCMS INSTALLATION FAILED'
			mail to: 'ravi.al.kumar@oracle.com,monal.kumar@oracle.com',
             		     subject: "OCMS Installation Failed",
             		     body: "OCMS Setup Failed.\n\nPlease check the previous mails to know further details\n\n\n\n\n\nRegards,\nCloud Enablement Team"										
		}		
	}
}
