# VPC-Networks-1
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
