# VPC-Networks-1
------------------------------------------------------------------------
creating a subnet
-------------------------------------------------------------------------------
gcloud compute networks create managementnet --project=qwiklabs-gcp-03-e1b085560f61 --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional

gcloud compute networks subnets create managementsubnet-us --project=qwiklabs-gcp-03-e1b085560f61 --range=10.130.0.0/20 --network=managementnet --region=us-central1
---------------------------------------------------------------
Creating a privatenet network
---------------------------------------------------------------------------
gcloud compute --project=qwiklabs-gcp-00-c7314351edd5 firewall-rules create managementnet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=managementnet --action=ALLOW --rules=tcp:22,tcp:3389,icmp --source-ranges=0.0.0.0/0
------------------------------------------------------------------------------
create the firewall
--------------------------------------------------------------------------------
gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0
------------------------------------------------------------------------------------------------
Run the following command to list all the firewall rules (sorted by VPC network):
---------------------------------------------------------------------------------------------
gcloud compute firewall-rules list --sort-by=NETWORK
-----------------------------------------------------------------------------------------------------
In Cloud Shell, run the following command to create the privatenet-us-vm instance:
------------------------------------------------------------------------------------------------------------
gcloud compute instances create privatenet-us-vm --zone=us-central1-f --machine-type=n1-standard-1 --subnet=privatesubnet-us
