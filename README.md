# RemoteGitDiploy

##### Description
This is a simple bash script that will help you to push your code to a web server via *'git push'* so you would not need to use any other SFTP client to do the file synchronization. 

It works by initializing a bare git repository on a linux machine. Once the repo is initialized you can add it as a remote to your local git repo and push your changes to the server via SSH. 
##### What you need
**Server:** git installed, SSH enabled linux server. Optional curl installation needed to get the public IP of server.
<br>
**Client:** git & SSH client installed. 
##### How to use RemoteGitDiploy
###### Step 1 - Getting remoteGitDeploy
Install remoteGitDeploy on your sever. First login to your server (via ssh) and pull a copy of this repo to a directory. 
<br> 

    git clone https://github.com/wik2kassa/RemoteGitDeploy.git
###### Step 2 - Installing remoteGitDeploy (Optional)
You can optionally install remoteGitDeploy on your server. First cd into the repo directory and run this command. 

    cd RemoteGitDeploy
Then run the following command (you most probably would need to run this as root)

    sh ./gitdeploy install 
This will install gitdeploy as an executable to your /bin folder. 
###### Step 3 - Creating repo on server
Create a repository on your server using the following command: 
<br>

If you have installed gitDeploy:

    gitdeploy <path to your server git repo> <path to your production code>
If you did not install gitDeploy: 

    ./gitdeploy <path to your server git repo> <path to your production code>
<br>

example:

    gitdeploy /home/ubuntu/mygitrepo /var/www/html/myproductionlocation
*This will create a git repo in home folder called mygitrepo and will copy code to* **/var/www/html/myproductionlocation** *whenever new commits are pushed to the server.*
###### Step 4 - Do your first git push from the client
After step 3 is done gitDeploy will give you the list of commands to execute on your client to start pushing data to your server. Basically what you have to do is add your remote servers repo as a remote for your git repository. 
<br>
Goto the folder of your git repository or create a new git repository using git init. And add your new repository as a remote

    git remote add production ssh://<username>@<host ip/ host domain>/<remote location>

in our example this would be something like this:

    git remote add production ssh://ubuntu@192.168.1.2/home/ubuntu/mygitrepo
    
##### Notes
* Make sure you add your ssh keys to known_hosts ssh files 
* gitDeploy will not correctly identify the public IP of some shared hosting accounts with SSH support. 



##### Advantages over syncing files via SFTP
* No need of a separate SFTP file upload client to push code to a production server. 
* Bandwidth & time saving, because  diff delta pack files are uploaded and not individual files are uploaded. 
* Easily do and track changes to code on local repo and production.

##### Thanks 
* Jeff Heoff's great tutorial on the process of using git as a deployment tool. <a href='http://www.jeffhoefs.com/2012/09/setup-git-deploy-for-aws-ec2-ubuntu-instance/'>Check it out here</a>.

##### Comments, bug-fixes and feedback are more than appreciated.



