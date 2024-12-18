
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>What I Learned From Exploring osTicket</h1>

<h3><b>Admin Panel vs Agent Panel</b></h3>
<p><b> Admin Panel </b></p>
<p>In the Admin Panel there are more backend configuration as shown in the photo below.The Agent Panel is tailored for support agents who handle tickets and interact with users. Things admin are capable of doing are:</p>

- Configuring Roles: Assigning/Creating roles for agents or departments. Adjusting diffrent type of permissions for each role. 
- Configuring Departments: Assigning/Creating departments 
- Configuring Team and Agent settings: Adding new or removing agents on diffrent teams.
- SLA Configurations: Adding grace time periods for diffrent Severity level ratings. 
<img src="https://github.com/user-attachments/assets/95d1d392-295d-4c73-9211-30b088d8ff76" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p><b> Agent Panel </b></p>
<p>The Agent Panel is more focused on day-to-day ticket handling and communication. It’s for agents who resolve tickets and assist users.</p>

- Configure users
- Configure Help Topics
<img src="https://github.com/user-attachments/assets/65fada69-f429-421b-94c3-a0b200705b5d" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h2>Installation Steps</h2>


<p>
<img src="https://github.com/user-attachments/assets/a7951c34-3cc6-4978-a9cc-1657848e9f2a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/6c4a18bf-0d44-4a78-91e7-b2bcc126f724" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First we need to Install / Enable IIS in Windows WITH CGI. IIS (Internet Information Services) is the web server needed to host osTicket, and CGI allows IIS to execute PHP scripts.
  
  1.  Navigate to Control Panel > Programs > Programs and Features and head into "Turn Windows Features on or off"
  2.  Check the box "internet infortmation services (ISS)"
  3.  Expand ISS -> Expand "World Wide Web Services" -> Expand "Application Development Feature" -> Check the box "CGI"
  4.  Press "OK" to continue with the installation 



</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/42032a4d-7bfe-45cc-a388-63ddcb491b34" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Then we head into the unzipped "osTicket-Installation-Files" file we had installed onto the VM's desktop and install "PHP Manager" for IIS. PHP Manager simplifies the process of registering and managing PHP within IIS.
</p>
<p>
Within the same file you will have to also install IIS Rewrite Module (rewrite_amd). The Rewrite Module enables URL rewriting, which is required for clean and user-friendly URLs in osTicket.
</p>

<br />

<p>
<img src="https://github.com/user-attachments/assets/8bc7a7cc-73cc-4f8f-8b00-5e322827a07f"/>
</p>
<p>
Create a new directory on the C:Drive named "PHP". Then from the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder.
</p>
<p>
Install Visual C++ Redistributable (VC_redist.x86.exe) and MySQL 5.5.62 (mysql-5.5.62-win32.msi) from the installing files. The Visual C++ Redistributable is required for PHP and MySQL to function correctly on Windows and MySQL is the database management system osTicket uses to store its data.

</p>
<p>
  When Installing MySQL 5.5.62 
  
1.  Select "Typical" when choosing a setup type.
2.  Select "Standard Configuration" when choosing the configuration type.
3.  During the secuirty options, enter "root" as the password for simplicity.
4.  MySQL is now ready to be excuted.
      
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/c76e77ec-4a67-4656-938c-ffd30217a091" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/3d8f81f0-87ce-44bd-80ac-89b20bad9aea" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open IIS as Administrator, then use PHP Manager to register PHP. Path: C:\PHP\php-cgi.exe. This links PHP to IIS, enabling PHP scripts to run on the web server. Afterwards reload IIS by stopping/starting the server in Manage Server. Reloading IIS applies all new configurations and ensures services are ready.
</p>
<p>
  Return back to "osTicket-Installation-Files" and unzip "osTicket-v1.15.8.zip". 

  - Copy the "upload" folder to C:\inetpub\wwwroot
  - Rename the "upload" folder to "osTicket"
  - Afterwards reload IIS by stopping/starting the server in Manage Server again.
</p>
<p>The osTicket files must be placed in the IIS root directory for the web server to serve them.
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/1cd2fe06-d1dd-4ead-bfdf-640ddfe77274" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/dc5e5fba-a707-4150-8cf6-65e458a1a731" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Then on the IIS Manager, Navigate to Sites → Default → osTicket and click “Browse *:80.”.  This verifies osTicket is accessible and identifies any missing PHP extensions. As shown on the second photo, some PHP extensions are not enabled.
</p>
<p>
  To enable the PHP extenstions, head back to the IIS Manager and Navigate to Sites → Default → osTicket then head to "PHP Manager" and click on "Enable or disable extensions". Enable the following extensions:

  - php_imap.dll
  - php_intl.dll
  - php_opcache.dll
<p>
  These extensions are required for osTicket's full functionality (e.g., email, internationalization, and caching).
</p>

</p>
<br />
<p>

<img src="https://github.com/user-attachments/assets/b1926a65-481a-4642-80ce-9e0f990557a8" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/d205992a-068c-4d40-97f2-46bf8cf42b0b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/0a4b4d97-aedb-448f-90cd-de6a8b3fd959" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Rename Configuration File "into ost-config.php". Navigate to the C:Drive inetpub > wwwroot > osTicket > include. Find the file named "ost-sampleconfig.php" and rename it to "ost-config.php". osTicket requires this file to store its configuration settings.
</p>
<p>
  Afterwards, we have to assign Permissions to ost-config.php
  
  - Disable inheritance → Remove all existing permissions.
  - Add new permissions: Everyone → All.
</p>
<p>
  Proper permissions allow osTicket to write to this file during installation.

</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/58ecb3d7-21d5-40c0-bc5e-34f902de6e16" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 Continue Setting Up osTicket in the Browser, provide details like the helpdesk name and default email. This step initializes osTicket’s basic configuration. 
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/0c55d5f9-2c0d-40c3-8509-cf24faa5336f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/0c0c96c1-44c3-42d6-b69a-bc55ab91d34b" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
From the “osTicket-Installation-Files” folder, install HeidiSQL, HeidiSQL simplifies database management, and the osTicket database is essential for storing osTicket data.

  - Open Heidi SQL
  - Create a new session, root/root
  - Connect to the session
  - Create a database called “osTicket”
<p>
   Finalize osTicket Setup in the Browser by providing MySQL credentials:

  - Database: osTicket
  - Username: root
  - Password: root
  - Finally click "Install Now"
</p>
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/5233fbb8-6d36-4761-b5b9-14144521e847" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/2ccbffe5-5390-4792-b723-c5a6b33a4d99" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Congratulations, hopefully it is installed with no errors!

- Browse to your help desk login page: http://localhost/osTicket/scp/login.php
- End Users osTicket URL: http://localhost/osTicket/ 

</p>
<br />
