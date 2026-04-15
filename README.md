### Ansible Project Documentation                                                                                                                                                             
                                                                                                                                                                                               
 #### Overview                                                                                                                                                                                 
                                                                                                                                                                                               
 This documentation outlines the structure and configuration of the Ansible project used for managing various Proxmox nodes and Debian guests.                                                 
                                                                                                                                                                                               
 #### Directory Structure                                                                                                                                                                      
                                                                                                                                                                                               
 - /home/martin/ansible/                                                                                                                                                                       
     - Contains inventory files and playbooks for managing virtualization environments.                                                                                                        
                                                                                                                                                                                               
 #### Inventory File: inventory.ini                                                                                                                                                            
                                                                                                                                                                                               
 This file contains host definitions and variables for accessing the Proxmox nodes and Debian virtual machines (VMs) and Linux Containers (LXCs).                                              
                                                                                                                                                                                               
 Sections:                                                                                                                                                                                     
 - [proxmox_hosts]: Lists the Proxmox nodes                                                                                                                                                    
     - pve1: Proxmox node with IP 192.168.68.84                                                                                                                                                
     - pve2: Proxmox node with IP 192.168.68.85                                                                                                                                                
 - [debian_vms]: Lists the Debian virtual machines                                                                                                                                             
     - dockerhost: Debian VM with IP 192.168.68.100                                                                                                                                            
 - [debian_lxcs]: Lists the Debian Linux Containers                                                                                                                                            
     - traefik: Debian LXC with IP 192.168.68.70                                                                                                                                               
 - [debian_guests:children]: Groups both VMs and LXCs under a single section for easier management.                                                                                            
                                                                                                                                                                                               
 Variables for All Hosts:                                                                                                                                                                      
 - ansible_user: The SSH user (openclaw) used for accessing all hosts.                                                                                                                         
 - ansible_ssh_private_key_file: The file path to the private SSH key used for authentication.                                                                                                 
 - ansible_become: Enables privilege escalation.                                                                                                                                               
 - ansible_become_method: Specifies the method of privilege escalation (set to sudo).                                                                                                          
                                                                                                                                                                                               
 #### Playbooks                                                                                                                                                                                
                                                                                                                                                                                               
 - Update Playbook(s): Define playbooks for updating hosts, ensuring that they have the latest software and configurations. Include tasks related to rebooting if necessary.                   
                                                                                                                                                                                               
 ### Usage Instructions                                                                                                                                                                        
                                                                                                                                                                                               
 1. Run a Playbook: To execute a playbook, use the command:                                                                                                                                    
   ```bash                                                                                                                                                                                     
     ansible-playbook -i inventory.ini <playbook_name>.yml                                                                                                                                     
   ```                                                                                                                                                                                         
 2. Check Host Connectivity:                                                                                                                                                                   
 Test SSH connectivity to all hosts defined in the inventory using:                                                                                                                            
   ```bash                                                                                                                                                                                     
     ansible all -i inventory.ini -m ping                                                                                                                                                      
   ```                                                                                                                                                                                         
                                                                                                                                                                                               
 ### Notes                                                                                                                                                                                     
                                                                                                                                                                                               
 - Make sure that the public key associated with the ansible_ssh_private_key_file is added to the ~/.ssh/authorized_keys file on all managed hosts.                                            
 - Ensure that the Ansible version is compatible with the YAML syntax used.     
