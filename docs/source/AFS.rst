.. image:: /Images/NC_State.gif
   :target: http://www.ncsu.edu


.. role:: bash(code)
   :language: bash



Setup FileZilla To Connect To K Drive/AFS Home Drive 
====================================================

Installing FileZilla
********************

Download FileZilla for free from the project’s website:

`https://filezilla-project.org <https://filezilla-project.org>`_

 

Configuring FileZilla
*********************

1.	For “Host:” enter: sftp://remote.eos.ncsu.edu
2.	For “Username:” enter: your Unity ID (ex. jdoe3)
3.	For “Password:” enter: your Unity ID Password
4.	For “Port:” you can leave blank.
5.	The first time you connect, you will get a pop-up “Unknown host key.” Select the checkbox to “Always trust this host, add this key to the cache”
6.	If successful, in the right window pane under “Remote site:” you will see the contents of your K: drive/home AFS space.
7.	To save your connection, select File > “Copy current connection to Site Manager…”
8.	Give it a friendly name like “K:”
9.	To reconnect, click on the Site Manager button in the toolbar and select your K: drive.

\ 


Alternatively, you can setup the connection using the site manager to remember your settings.

1.	Go to File > Site Manager…
2.	Click on the “New Site” button.
3.	Type a name for the site, for you K: drive enter “K:” or any other friendly name.
4.	For “Host:” enter: remote.eos.ncsu.edu
5.	For “Port:” you can leave blank.
6.	For “Protocol:” choose “SFTP  SSH File Transfer Protocol” from the drop-down.
7.	For “Logon Type:” choose “Ask for Password” from the drop-down.
8.	For “Username:” enter: your Unity ID (ex. jdoe3)
9.	Click the “Connect” button to test your connection.
10.	The first time you connect, you will get a pop-up “Unknown host key.” Select the checkbox to “Always trust this host, add this key to the cache”
11.	If successful, in the right window pane under “Remote site:” you will see the contents of your K: drive/home AFS space.
12.	To reconnect, click on the Site Manager button in the toolbar and select your K: drive.


Transferring files to AFS drive  
*******************************


To transfer, just drag the desired file into the bottom-right box once connected to AFS in filezilla (see image below). The file should now be accessible via SSH connection.
 
		*It's recomended that you make a new folder within the AFS labeled: "BIT815" to keep all the files in one place.*


	.. image:: /Images/Filezilla.png
   


`Source <https://www.itecs.ncsu.edu/servicedesk/kb/setup-filezilla-to-connect-to-k-driveafs-home-drive/>`_
Last modified 9 January 2019.
Edits by `Ross Whetten <https://github.com/rwhetten>`_, `Will Kohlway <https://github.com/wkohlway>`_, & `Maria Adonay <https://github.com/amalgamaria>`_.
