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
				
							
			}
		}
		stage('5.Vault Installation') 
		{
			steps 
			{				
				bat 'echo "Step 5"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					rem plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\install_vault.txt llg00fic.uk.oracle.com
				'''
				winRMClient credentialsId: 'llg00fgg.uk.oracle.com_ORADEV\\\\kurravi_1541753948', hostName: 'llg00fgg.uk.oracle.com', winRMOperations: [invokeCommand('cd /d C:\\chef'),invokeCommand('chef-client')]				
			}
		}        
		stage('6.llg00fgg.uk.oracle.com Prerequisites') 
		{
			steps 
			{
				bat 'echo "Step 6"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\ocms_prerequisites.txt llg00fic.uk.oracle.com
				'''
				winRMClient credentialsId: 'llg00fgg.uk.oracle.com_ORADEV\\kurravi_1541753948', hostName: 'llg00fgg.uk.oracle.com', winRMOperations: [invokeCommand('cd /d C:\\chef'),invokeCommand('chef-client')]				
			}
		}
		stage('7.DB Installation') 
		{
			steps 
			{
				bat 'echo "Step 7"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\install_db.txt llg00fic.uk.oracle.com
				'''
				winRMClient credentialsId: 'llg00fgg.uk.oracle.com_ORADEV\\kurravi_1541753948', hostName: 'llg00fgg.uk.oracle.com', winRMOperations: [invokeCommand('cd /d C:\\chef'),invokeCommand('chef-client')]				
			}
		}
		stage('8.MI Domain Creation') 
		{
			steps 
			{		
				bat 'echo "Step 8"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\install_mi.txt llg00fic.uk.oracle.com
				'''
				winRMClient credentialsId: 'llg00fgg.uk.oracle.com_ORADEV\\kurravi_1541753948', hostName: 'llg00fgg.uk.oracle.com', winRMOperations: [invokeCommand('cd /d C:\\chef'),invokeCommand('chef-client')]				
			}
		}
		stage('9.Starting Servers') 
		{
			steps 
			{
				bat 'echo "Step 9"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\start_admin.txt llg00fic.uk.oracle.com
				'''
				winRMClient credentialsId: 'llg00fgg.uk.oracle.com_ORADEV\\kurravi_1541753948', hostName: 'llg00fgg.uk.oracle.com', winRMOperations: [invokeCommand('cd /d C:\\chef'),invokeCommand('chef-client')]				
			}
		}
		stage('10.llg00fgg.uk.oracle.com Deployments') 
		{
			steps 
			{
				bat 'echo "Step 10"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\install_ocms.txt llg00fic.uk.oracle.com
				'''
				winRMClient credentialsId: 'llg00fgg.uk.oracle.com_ORADEV\\kurravi_1541753948', hostName: 'llg00fgg.uk.oracle.com', winRMOperations: [invokeCommand('cd /d C:\\chef'),invokeCommand('chef-client')]				
			}
		}
		stage('11.Restarting All Servers') 
		{
			steps
			{
				bat 'echo "Step 11"'
				bat '''
					cd /d C:\\Program Files\\PuTTY
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\start_all_servers.txt llg00fic.uk.oracle.com
				'''
				winRMClient credentialsId: 'llg00fgg.uk.oracle.com_ORADEV\\kurravi_1541753948', hostName: 'llg00fgg.uk.oracle.com', winRMOperations: [invokeCommand('cd /d C:\\chef'),invokeCommand('chef-client')]				
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
					plink -ssh -l hgbu -pw hgbu -m C:\\chef-repo\\llg00fgg.uk.oracle.com_files\\Revertchange.txt llg00fic.uk.oracle.com
			'''
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
