# About

This is a clone repository from [Ola Hallengren's SQL Server Maintenance Solution](http://ola.hallengren.com/)

# [License](http://ola.hallengren.com/license.html)

# Schedule

By default the jobs are not scheduled, that's why in this repo you'll find several t-sql scripts to schedule the maintenance jobs.

> So how should you schedule these new maintenance jobs? The answer depends on your maintenance window, the size of your databases, the maximum data loss you can tolerate, and many other factors. Here are some guidelines that you can start with, but you will need to adjust these to your environment.
> I recommend that you run a full backup after the index maintenance. The following differential backups will then be small. I also recommend that you perform the full backup after the integrity check. Then you know that the integrity of the backup is okay.
> [Reference](http://ola.hallengren.com/frequently-asked-questions.html)

## User databases

Full backup one day per week
Job Name: DatabaseBackup - USER_DATABASES - FULL
Execute on sunday at 21:00

Differential backup all other days of the week
Job Name: DatabaseBackup - USER_DATABASES - DIFF
Execute on Monday to saturday at 21:00

Transaction log backup every hour
Job Name: DatabaseBackup - USER_DATABASES - LOG
Execute at 06:00

Integrity check one day per week
Job Name: DatabaseIntegrityCheck - USER_DATABASES
Execute on sunday at 20:00

Index maintenance one day per week
Job Name: IndexOptimize - USER_DATABASES
Execute on sunday at 19:00
		
## System databases

Full backup every day
Job Name: DatabaseBackup - SYSTEM_DATABASES - FULL
Execute at 23:00 

Integrity check one day per week
Job Name: DatabaseIntegrityCheck - SYSTEM_DATABASES
Execute on sunday at 22:00
		
## Cleanup

sp_delete_backuphistory one day per week
Job Name: sp_delete_backuphistory
Execute on monday at 04:00 
	
sp_purge_jobhistory one day per week
Job Name: sp_purge_jobhistory
Execute on monday at 04:00 
	
CommandLog cleanup one day per week
Job Name: CommandLog Cleanup
Execute on monday at 04:00 
	
Output file cleanup one day per week
Job name: Output File Cleanup
Execute on monday at 04:00 
