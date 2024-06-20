# Deploying a Simple Webpage on Azure using a Virtual Machine
---

# Table of Contents
1. [Introduction](#introduction)
2. [Prerequisite](#prerequisite)
3. [Step-by-Step Guide](#step-by-step-guide)

## Introduction
In this project, I will deploy a simple webpage on Microsoft Azure, utilizing Azure compute and network services. The goal is to give me hands-on experience with provisioning and configuring virtual machines (VMs), setting up networking components, and deploying a web app.

## Prerequisite
Before starting this project, ensure you have the following:
- An Azure account. You can sign up for a free account [here](https://portal.azure.com/).
- Basic knowledge of web development.
- Access to a web browser.
- An application or webpage ready for deployment


## Step-by-Step Guide
### Provisioning a Virtual Machine
1. Login to the [Azure Portal](https://portal.azure.com/)
2. In the Azure portal dashboard, click on __Create a resource__ in the upper-left corner.
   ![1b](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/22e73fbe-0006-4985-b8f5-b028713e13b2)

3. Search for __Virtual Machine__ and select __Virtual Machine__ from the search results OR 
Click on __Create Resource__ then select __Virtual Machine__ from the list of resources.
   ![1a](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/a0af8583-87bb-4efa-84cb-11f9319e229b)

4. On the __Basics__ tab, Select an Azure subscription and Resource Group in the project details section. Then In the instance details section give the VM a unique name, select a region in this case I used __South Africa North__ because it is closer to my country, chose an availability option and zone.
   ![2](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/17b97d31-7eb2-42be-91c1-ca498b92b107)

5. Select the security type, Image (basically the operating system, I chose ubuntu), VM architecture and VM size. For the VM size I chose to use a B series size because they are cheap and use lesser resources, which is enough for my single webpage deployment.
   ![3](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/47a12935-b52a-4f0e-91d5-da56f1227604)

6. For the  virtual Machine authentication type, I selected __password__, I set my public inbound ports to __Allow selected ports__and selected the inbound ports.
    ![4](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/54ecd251-9bd4-4085-99ed-b2d36840d7da)

7. On __Disks__ tab, I used the default image OS disk size, selected the __standard SSD (locally-redundant storage)__ as OS disk type because Standard SSD is the best for web servers lightly used enterprise applications and dev/test, also using locally redundant storage because the project is not serious enough that it only requires data to be replicated within a single datacenter.
    ![5](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5e87a1fa-fcdc-4fbf-9359-82730faab929)

8. I chose __platform managed key__ for key management because with PMKs, the keys generated are stored and managed by Azure.
    ![6](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/d189082c-359e-4992-87af-021705aa9ca5)

9. On the __Networking__ tab, I left everything at default in the Network Interface section.
    ![7](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/6e0c6e6f-0cba-4e60-acd2-2cce601de9bc)

10. I enabled __Delete public IP and NIC when VM is deleted__ and selected __None__ for load balancing option as my single webpage would not be recieving traffic that would require any load balancer.
    ![8](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5c5f0a28-333c-4a5e-bd55-689aeec532a9)

11. On __Management__ tab, everything was left at default.
    ![9](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/30815995-9d1a-400c-a8d5-d231e37fa463)

12. On __Monitoring__ tab, I chose __Enable with managed storage account__ as the boot diagnostics.
    ![10](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/b43dac8b-efb9-4a86-bac6-1635f3031194)

13. Select the __Review + Create__ tab.
    ![12](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/c190d398-dac0-415b-9902-8f099dcac902)

14. Once VM configuration is satisfactory select __Create__.
> YAAYYY!! the Virtual Machine has been provisioned.
![14](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/3c3000bb-81b1-455c-b410-3b0247d0098e)


### Connect to the Virtual Machine
> A VM can be connected to using SSH (for Linux VMs) or RDP (for Windows VMs)
1. Go to the virtual machine that was provisioned.
   ![15](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/b8ac7d2a-35a7-4740-ba31-7a7b1a2cf9dd)

2. click on __Connect__.
   ![16](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/3ac9fa94-efff-490d-9ac7-45d07968a325)

3. Select a tool for connecting. I chose the __SSH using Azure CLI__.
   ![17](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/65f6e8ba-7042-42f9-8480-9db998c98823)

4. Configure it and connect.
   ![18](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/d8570ad5-d1b9-4ccc-9744-5ed2cc8c9f1b)

5. A CLI would appear, I chose __Bash__ as the CLI .
    ![19](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/cb425ed4-35d1-4627-a815-1ea6ee3bf093)

6. In the CLI use the code, to connect
``` 
ssh username@public_ip_address
```
    ![22](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/a14d73d8-353b-488b-904b-4a122bec4710)

7. Key in the VM password.
    ![23](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/01f6fcea-87b8-49e9-9788-d6ac6d6b60ef)

### Install and Configure a Webserver
Install a web server software on your VM. Common choices include Apache, Nginx, or IIS. For this project i used `Apache` webserver.
1. Update the package index and install Apache web server.
```
sudo apt-get update && sudo apt-get install apache2
```
2. Configure the web server to serve the web page files. For Apache, you'd typically place your files in the `/var/www/` directory.

### Transfer Webpage files
Tools like SCP, WinSCP, Git or FTP can be used to upload files. Since my webpage is already on GitHub, I would clone the repository to the `/var/www` directory.
1. Move into the `www` directory from thr oot directory.
```
cd /var/www
```
3. Clone the repository.
```
sudo git clone https://github.com/oputaolivia/Azure-Virtual-Machine.git
```
5. Move into the Azure-Virtual-Machine directory.
```
cd Azure-virtual-Machine
```
7. Set Permissions.
```
sudo chmod -R 755 /var/www/
```


### Deploying a Webpage
To actually have our webpage served, we need to ensure that Apache is configured to serve the specific webpage.
1. Change directory to the root directory and navigate to the `sites_available` folder to see the `000-default.conf` file.
```
cd ../../etc/apache2/sites-available
```
3. Using Vim open the `000-default.conf file
```
sudo vim 000-default.conf
```
5. Edit the config file by changing the DocumentRoot from `/var/www/html` to `/var/www/Azure-Virtual-Machine` then save and quit.
6. Before accessing the website, it's a good idea to test the Apache configuration to ensure there are no syntax errors.
```
sudo apache2ctl configtest
```
8. If there are no errors, restart the Apache service to apply the changes.
```
sudo systemctl restart apache2
```

> Now the webpage is accessible via my public address http://4.222.184.194
![30](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f252ec39-8f2e-4eda-8558-d087ddb81a7e)
