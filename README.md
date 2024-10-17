# About
LogonLog is a lightweight software tool designed to read a database containing logon and logoff events. These events are logged via a batch script (logonlog.bat) that is set up in Group Policy as a logon and logoff script. The scripts utilize the SQLite libraries to store the logs in an organized format.
The program itself serves as a viewer for the batch script logs but can also assist in setting up the program.

# First Run

First run will need to be run as Administrator, please ensure this is done so that any setup steps are able to complete. Upon the first run, the program will automatically create an SQLite folder and place the required SQLite.exe file inside it. This file is essential for both the main program and the batch script.

Once the program is running, you will have the option to open an existing database, which can be located anywhere as long as it contains the necessary data.

To access the settings, click the cog icon in the top-right corner. You will be prompted for a password. The default password is hard-coded as LogonLog, serving as a preventive measure to ensure that general users do not make accidental changes or run the setup process unintentionally.

# Setup

When the settings are opened, you will see a button labeled "Setup Program." This button is designed to simplify the setup process. Clicking it will:
- Create the required folder structure.
- Share the root folder from its current location.
- It will create a hidden share \\HOSTNAME\LogonLog$ that is accessible for viewing by all users.
- Ensure the DB folder is present and create the database file (log.db) within this folder, while setting the correct permissions (read/write access for Domain Users).
- Check for the SQLite binaries, and if they are missing, add them.
- Create a new GPO folder with instructions for setting up the necessary Group Policy Objects.
- Generate a config.txt file that contains the correct database location based on the current setup.
- Create the batch script (LogonLog.bat), ensuring it is in the correct folder and will not encounter errors when reading the config file.

# Main Program
The main program automatically loads the database defined in the config.txt file created during the setup. This streamlines usage and prevents the user from having to manually open the database each time. However, you can still open another database using the "Open Database" button at the top of the window if necessary.

## Filtering
Once the database is loaded, you can filter the events by server name, event type, username, date, and time. To remove all filters, click "Clear Filters." 

## Exporting Results
After filtering the results, you can export them to a CSV file. This is useful for generating reports on specific users or servers. To do this, click the "Export CSV" button, select a location, and save the file.

## LogonLog includes an auto-update feature to ensure you are always running the latest version. When you open the program, you will be prompted if an update is available.
-	If you choose "Yes", the program will close automatically and begin the update process. Once the update is complete, you can relaunch the program with the latest version.
-	If you choose "No", the program will continue to run without updating, allowing you to use the current version as normal.

## Batch Script
The batch script is responsible for logging logon and logoff events. It works with Group Policy and the SQLite libraries to store each event in the central database. The location of the database is defined in a config file (config.txt).
A typical folder structure for this setup is:
-	logonlog.bat  
-	config.txt  
-	SQLite/  
o	SQLite.exe  
-	DB/  
o	log.db  

## Switches
The batch script uses two switches: logon and logoff. These specify the action to be logged. The switches can be run manually as follows:
-	logonlog.bat /logon - Logs a logon event.
-	logonlog.bat /logoff - Logs a logoff event.
