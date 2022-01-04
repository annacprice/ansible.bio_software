# ansible.bio_software
Installs the following:
* miniconda
* docker 
* singularity
* nextflow
* snakemake (in a conda environment)

## Install instructions
Install ansible
```
sudo apt-get update
sudo apt-get install ansible
```
Generate a ssh key pair
```
ssh-keygen
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
Update hosts file `sudo vim /etc/ansible/hosts`, adding the following
```
[test]
IP-ADDRESS-HERE
```
Update ansible config file `sudo vim /etc/ansible/ansible.cfg`, adding the following
```
[defaults]
inventory = /etc/ansible/hosts
remote_user = ubuntu
private_key_file = ~/.ssh/id_rsa 
```
Clone the repo
```
git clone https://github.com/annacprice/ansible.bio_software.git
```
Run the playbook
```
cd ansible.bio_software
ansible-playbook playbook.yml
```
Once the ansible playbook has finished running, the $PATH will need to be reloaded (e.g. start new login shell or use `source`)

### Checking install
Suggested commands to check the software has installed correctly
```
docker run hello-world:latest
singularity pull library://sylabsed/examples/lolcow
singularity exec lolcow_latest.sif cowsay moo
conda activate
nextflow -h
```
Snakemake is available through a conda env
```
conda info --envs
conda activate snakemake
snakemake -h
```
