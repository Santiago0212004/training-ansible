### Santiago José Barraza Sinning

### Ingeniería de Software V

# Terraform + Ansible

## Exercise

![](images/1.png)

At first, a `terraform init` was executed, which allows downloading the providers that are going to be used to build the infrastructure (in this case, Azure).

![](images/2.png)

Then, a `terraform plan -out main.tfplan` was performed to verify that everything is correct and the infrastructure can be built.  

![](images/3.png)

After that, `terraform apply main.tfplan` was executed, which applies and builds the infrastructure according to the plan that was made.

![](images/4.png)

It can be seen that the infrastructure was built correctly, and the output provides the public IP address of the virtual machine and the name of the resource group.

![](images/5.png)

Then, the SSH connection was tested, and it was confirmed to be working correctly.

![](images/6.png)

The hosts.ini IP address of the Azure machine was changed to allow Ansible to connect to the VM and make the necessary configurations.

![](images/7.png)

After that, `ansible-playbook -i inventory/hosts.ini playbooks/install_docker.yml` was executed. This executed the Ansible playbook that installs Docker in the VM, and it did so successfully.

![](images/8.png)

Then, another Ansible playbook was executed in the same way. The objective of `run_container.yml` was to create a Docker container that runs a Mario game and expose it on port 8787.

![](images/9.png)

Then, another rule was created for the security group to allow HTTP traffic on port 8787, making the game available and accessible through the internet.

![](images/10.png)
![](images/11.png)

A `terraform plan` was made again, and it could be seen that the rest of the infrastructure would remain the same, with the only change being on the security group rules.

![](images/12.png)

Then, `terraform apply` was successfully executed, which means that the rules of the security group were correctly changed.

![](images/13.png)

It was verified that the game was correctly deployed in the container and the port was accessible through the internet.

![](images/14.png)

The game was playable and working correctly.

![](images/15.png)

Finally, a `terraform destroy` was executed to delete all the infrastructure that was created in this exercise, so it would not generate more costs in the Azure account.

## Conclusion

IaC tools like Terraform allow engineers to set up infrastructure in a repeatable process that can be iterated when a change is needed, without changing everything else. These tools provide the possibility of versioning the different states of the infrastructure, and the infrastructure can be easily destroyed, allowing resources to be managed in an efficient way. On the other hand, Configuration Management tools like Ansible allow the creation of automated scripts (playbooks) that can quickly configure the infrastructure that is already set up, so engineers don't need to configure every machine individually and manually, as this process is automated.
