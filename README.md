# Azure-Firewall-Service
Deploy the Azure Firewall Service and Create Route

The Azure Firewall is a stateful firewall, meaning it monitors the full state of network connections and is constantly analyzing network traffic and packet data. It must be deployed to a Virtual Network with a subnet named AzureFirewallSubnet and must be at least /26 in size. This is because the Azure Firewall actually scales out with nodes based on demand and uses the AzureFirewallSubnet.  

In this lab step, you will deploy an Azure Firewall and add a route table to allow devices on an internal network to route to the Firewall.

Instructions

In the Azure portal, search for firewalls and click on the Firewalls  service:

![image](https://user-images.githubusercontent.com/58148717/112332511-cb0c8100-8c87-11eb-8c38-054ef4aa8523.png)

In the Create a firewall  menu, input the following values and click Review + Create:
	• Resource Group: Select the xx-xxx-xxx resource group in the drop-down list. 
	• Name: xxx
	• Region: Select the South Central US region
	• Firewall management: Select Use Firewall rules (classic) to manage this firewall
	• Choose a virtual network: Check the option for Use existing
	• Virtual Network: Select the xx-lab-vnet virtual network
	• Public IP Address: Select the pip-fw IP address

Now, a Route Table must be created to allow devices on the Internal-Network subnet to route all outbound traffic through the firewall:

![image](https://user-images.githubusercontent.com/58148717/112332726-fd1de300-8c87-11eb-87b3-25abffe11f73.png)

On the overview page of the firewall menu, note the private IP address of the firewall, this will be used in a later step.

In the Azure portal, search for route tables and click on the Route tables service:

![image](https://user-images.githubusercontent.com/58148717/112332861-16bf2a80-8c88-11eb-97a3-f21834252eaf.png)

In the Create Route table  menu, input the following values and click Review + Create:
	• Resource Group: Select the xxx-xxx-xx resource group in the drop-down list
	• Region: Select the South Central US region
  
Click Create to start deploying the route table

On the left-hand side click Subnets and click the Associate button

In the Associate subnet  menu, input the following values and click OK:
	• Virtual Network: Select xxx-xx-vnet in the drop-down list
  • Subnet: Select Internal-Network
  
On the left-hand side click Routes and click the Add button:

![image](https://user-images.githubusercontent.com/58148717/112333267-73bae080-8c88-11eb-821d-3ef501b770f7.png)

The address prefix 0.0.0.0/0 means all traffic networks. So all traffic will route to the firewall's target IP address forcing all devices on the subnet to use the firewall.

Now lets create firewall rules

Go back to your firewall 

On the left-hand side select Rules  and click Add network rule collection  under the Network rule collection tab:

![image](https://user-images.githubusercontent.com/58148717/112333415-977e2680-8c88-11eb-9aa3-ee50d6b19b6f.png)

In the Add network rule collection  menu, input the following values

![image](https://user-images.githubusercontent.com/58148717/112333542-b2e93180-8c88-11eb-861b-ac8f63333521.png)


The network rule will allow all devices on the internal network (10.0.2.0/24) to use Google's public DNS service (8.8.8.8)

On the left-hand side click Public IP configuration and copy the public IP address of the Firewall

On the left-hand side select Rules  and click Add NAT rule collection  under the NAT rule collection tab

![image](https://user-images.githubusercontent.com/58148717/112333666-cc8a7900-8c88-11eb-8b60-d54a0e756a51.png)

The NAT rule will route external SSH traffic that connects to the public IP of the firewall to the  private IP address of the VM on the internal network (10.0.2.4)


In the Add application rule collection  menu, input the following values and click Add:

![image](https://user-images.githubusercontent.com/58148717/112333963-0c516080-8c89-11eb-8b3e-617cdefbfe8a.png)

This application rule will allow devices on the internal network to connect to google.com over HTTP or HTTPS



  
  



  


















