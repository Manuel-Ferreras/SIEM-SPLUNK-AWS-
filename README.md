# SIEM-SPLUNK-AWS-

<h3> Set up a Splunk server in secure AWS ec2(Amazon Elastic Compute Cloud) by setting role, security group(Firewall), ssh rules, securing my private key, created security alerts and reports to find Anomalies Integrated slack to get notified went the conditions are met. <h3>
 
 <h2> ec2 configuration </h2>

- Ubuntu AMI from quick start                                                           
- Instance type t2.micro free tier eligible
- key pair
  -  Key pair type = rsa
  -  privite key file format  pem for open shh use ( use to connect from my linux teminar) 
- networking  
  -  Create security group(Firewall)  allow  shh traffic from only my public IP and port 22 for ssh.
  -  Only allow the port number splunk enviriment is going to run.
  -  assign an elastic IP so you aways have the same public IP if you shut down your ec2 (is better to have a dynamic IP address for security over comfort).
  
- created an IAM role and give users enough Permission to use my ec2 Splunk server - following The principle of least privilege.
  
 <h2> Conneting to your ec2 </h2>
  
 - change permissions in you in your ec2 pair key using chmod because your key pair is unprotected  and it will not allow you to ssh into your ec2 with a weak permission. 
 
  <img src="https://i.imgur.com/vQUYDFL.png" height="40%" width="44%" alt=/> 
  
- Connect to my by you using this command shh -i (yourec2key) ec2-user@(youec2plublicip)
  
 <img src="https://i.imgur.com/aR7SMmb.png" height="40%" width="44%" alt=/> 
 
  <h2>Installing and configuring SPLUNK in a ec2</h2>
  
- You need to log in to your SPLUNK account and select the command line option to download. copy the Linux command and paste it into your terminal.

  <img src="https://i.imgur.com/2Gk6kNW.png" height="40%" width="44%" alt=/> 

- After downloading your file tar you download the file you use = tar -xvzf (name of your download file)
- Next you got to start Splunk from your bin directory using (./splunk start) and set username and password.

Then I went to my Splunk address web server the is going to be HTTP://(your ec2 public IP):(your assing port).
  
  <img src="https://i.imgur.com/JdJgW33.png" height="40%" width="44%" alt=/> 
  
  - To make my Splunk web server start at boot you got to type this commands in your bin directory.
    - ./splunk enable boot-start
    - systemctl enable splunk
    - sysmtemctl start splunk

 <h2> Slack Notification Alert </h2> 
 
 Integrated Slack Notification Alert to get notified of my Splunk alerts if conditions are met.

 <img src="https://i.imgur.com/O8PN9hd.png" height="40%" width="44%" alt=/>
 
 - Set up a dummy slack instance.
 - Install Slack Notification Alert Splunk plugging.
 - Install the incoming webhook in your slack instance.
     -  Added to your desired channel.
     -  Copied the URL of your webhook. 
 In Splunk got manage action >slack> Setup Slack Alerts >paste your webhook URL and save.
 - Can be used this be used in  sections Trigger Actions

<img src="https://i.imgur.com/PVOCOul.png" height="40%" width="44%" alt=/>

<h2>Created an alert that triggers if there is an unusually high number of failed login attempts.</h2>

 <img src="https://imgur.com/8wqjIpe.png" height="40%" width="44%" alt=/>

Set Trigger Conditions to numbers of results if condition is greater than 10 .
 
 <img src= "https://imgur.com/tObcU0q.png" height="20%" width="34%" alt=/>
 
Set the alert to notify me via Slack.

<img src= "https://imgur.com/obcPkwO.png" height="20%" width="34%" alt=/>

 

