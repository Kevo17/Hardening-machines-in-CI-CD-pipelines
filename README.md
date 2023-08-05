<h1>Hardening machinens in CI/CD pipelines</h1>


<h2>Description</h2>
This lab focuses on hardening machines within Continuous Integration/Continuous Deployment (CI/CD) pipelines using Ansible, ensuring that the infrastructure used for development and deployment processes is securely configured. By implementing security measures and best practices, organizations can reduce the risk of vulnerabilities and protect sensitive data throughout the software development lifecycle.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Ansible</b>
- <b>JSON</b>
- <b>GitLab</b>

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Linux</b> 

<h2>Program walk-through:</h2>

First, we need to install the Ansible program: <br/>
```
pip3 install ansible==6.4.0
``` 
<p align="center">
<img src="https://i.imgur.com/DUwt3ZK.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s create the inventory or CMDB file for Ansible using the following command: <br/>
 
<p align="center">
<img src="https://i.imgur.com/Euk7UjI.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Next, we will have to ensure the SSH’s yes/no prompt is not shown while running the ansible commands, so we will be using ssh-keyscan to capture the key signatures beforehand: <br/>
```
ssh-keyscan -t rsa prod-rcgsg0ei gitlab-ce-rcgsg0ei devsecops-box-rcgsg0ei >> ~/.ssh/known_hosts
``` 
<p align="center">
<img src="https://i.imgur.com/ngBQWrn.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

We will choose the dev-sec.os-hardening role from the dev-sec project to harden our production environment: <br/>
```
ansible-galaxy install dev-sec.os-hardening
``` 
<p align="center">
<img src="https://i.imgur.com/QaQ6YQf.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s create a playbook to use this role against a remote machine: <br/>
 
<p align="center">
<img src="https://i.imgur.com/g33Puce.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s run this playbook against the prod machine to harden it: <br/>
```
ansible-playbook -i inventory.ini ansible-hardening.yml
``` 
<p align="center">
<img src="https://i.imgur.com/by5XgVz.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Get priv key: <br/>
```
cat /root/.ssh/id_rsa
``` 
<p align="center">
<img src="https://i.imgur.com/uLyodVp.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Click on the Expand button under the Variables section in GitLab, then click the Add Variable button. Add the key/value pair in the form: <br/>
 
<p align="center">
<img src="https://i.imgur.com/vzBJBHd.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>
<p align="center">
<img src="https://i.imgur.com/OExgAZu.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s copy the hardening script to the GibLab files: <br/>
 
<p align="center">
<img src="https://i.imgur.com/ew5mbDz.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Click on the Edit button and append the following code to the .gitlab-ci.yml file: <br/>
 
<p align="center">
<img src="https://i.imgur.com/rDBSCnI.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

Here is the result of this job: <br/>
<p align="center">
<img src="https://i.imgur.com/y7ier5W.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
