# Online-Recharge
Deployment of website using Azure Services:

Project Description:

    The core idea of project is to solve the problem of web traffic. By using load balancer, it transfers web traffic over two servers. 
    If there was no load balancer, due to high traffic the website may get down. In this way, load balancer solve the problem of web traffic. 
    Load balancers improve application performance by increasing response time and reducing network latency. They perform several critical tasks such as the following: 
    Distribute the load evenly between servers to improve application performance. Redirect client requests to a geographically closer server to reduce latency.

Deployment Components :

    Linux VM : Ubuntu Server 20.04 LTS
    Compute Resources on : Azure
    Web Server : Apache2
    Web Front End : HTML

Deployment Steps
1st Step: Deploy Azure Compute Resource : Linux VM (Ubuntu 20.04)

-> Login to Azure Portal > Create a "Compute" Resource
-> Select Ubuntu Server 20.04 LTS > Create![vm1](https://github.com/kartik2181/Online-Recharge/assets/67506229/166a00bb-0746-4e45-889c-cd6af784dbd0)



-> Make sure you have selected
Username: azureuser and
SSH Key Pair Name: UbuntuVM_key
Click Review + Create 

-> Download Private Key and Create Resource


-> Finally, Azure side deployment is finished. Linux VM : "UbuntuVM" shows Running and provides a Public IP Address. It has configured and deployed all necessary components (Disk, Network I/F, NSG, Public/Private IP, etc) to run our Linux VM on Azure. 4.png

-> Using Putty Configuration and Port 22 for SSH (By default it is open. You can restrict it to only allow your Private IP to access port 22 using Network security group: "UbuntuVM-nsg"
-> While we are on the topic, We have to allow HTTP port 80 for Web Traffic as an Inbound Port rule in the Network Security Group.
-> Port 80 for Web and Port 22 for SSH is Open

    (Note : SSH is exposed to the internet and can be accessed from anywhere. For security best practices, it is NOT a recommended Nor valid practice. But for this Testing purposes, I have allowed it)
    5.png

->The Private Key we downloaded is important to Login into UbuntuVM (LinuxVM) we have created.
->Please follow below brief article on
Convert .Pem to .Ppk File Using PuTTYgen
Connect Linux VM using PuTTY
2nd Step : Login to Ubuntu , Install Apache2

-> Once the Putty PPK file is loaded to SSH into your Ubuntu VM
It will look like this.
xx.JPG -> I have used the Public IP address of UbuntuVM and .ppk file created using Putty Gen.
-> Opening it will allow us to log in to our Ubuntu Linux Server. As per,

3rd Step : Install Apache2 to make it a WebServer

-> Run below Command to update package

azureuser@UbuntuVM:~$ sudo apt update


-> Install Appache2 by Running below Command and Press "Y" to Continue...

azureuser@UbuntuVM:~$ sudo apt install apache2

 -> Once installed. Check its active (running) status by running,

azureuser@UbuntuVM:~$ service apache2 status

-> After verifying APACHE2 Web Server is running. Test the WebPage by going into your Browser and Paste your Ubuntu VM's Public IP Address. 10.png We successfully deployed our WebServer. Now its time to make it really ours. By changing the Front WebPage Index.html.
Currently, Public IP is showing Default Apache2 Ubuntu Default Page.
4th Step: Let's find the Index.html file and do some HTML Editing.

-> use cd to go to location /var/www/html

azureuser@UbuntuVM:~$ cd /var/www/html

-> ls command there will list the files inside that html directory. In this case it showed us index.html file. As per, 11.png
Important Process: -> 1. Remove existing index.html file by running sudo rm index.html -> 2. Create new index.html file by running sudo touch index.html 12.png

-> Edit the Index.html file by opening the file in vi editor using sudo

azureuser@UbuntuVM:/var/www/html$ sudo vi index.html

-> vi file editor will open. where you can paste your own HTML Code or follow mine (Copy below) whichever you want to make your Display Page (index.html) for your Web Server.

-> same process for second virtual machine.![vm2](https://github.com/kartik2181/Online-Recharge/assets/67506229/8d2c5022-bea3-4f9e-bccd-20721f85551c)

-> Then go to the Load balancer and add inbound rules to it.![Load_balancer](https://github.com/kartik2181/Online-Recharge/assets/67506229/a094886c-e387-4eca-9861-83e579314fc8)

-> Add DNS name lable to load balncer in Public ip address.![Public_IP](https://github.com/kartik2181/Online-Recharge/assets/67506229/f4a791c0-982f-4042-ba32-080f59225509)

# Final Step, Display our Webpage:
![Website](https://github.com/kartik2181/Online-Recharge/assets/67506229/98199172-b22a-49d8-870e-2f846a968302)





