# Ansible commands

    -C does a dry run, no actual changes


## Build
New Siege server, uses recipe in tasks/siege-rollout.yml

    ansible-playbook -c local -M modules -i files/inventory.ini tasks/siege-rollout.yml -C


## Install 
move settings on new Siege machines
NOTE: remove local connection

    ansible-playbook -M modules -i files/inventory.ini tasks/siege-install.yml -C


## Run 
siege based on settings in files/siege-siegesrc and files/siege-urls.txt
NOTE: remove local connection

    ansible-playbook -M modules -i files/inventory.ini tasks/siege-start.yml -C

## stop

    ansible-playbook -M modules -i files/inventory.ini tasks/siege-stop.yml -C

## file transfer
to move new configs up without running fill install process
    
### config

    ansible siege -m copy -i files/inventory.ini -a "src=files/siege-siegerc dest=/etc/siege/siegerc owner=root group=root mode=0644" -C

### URL's
    
    ansible siege -m copy -i files/inventory.ini -a "src=files/siege-urls.txt dest=/etc/siege/urls.txt owner=root group=root mode=0644" -C

### Get remote logs

    ansible siege -m fetch -i files/inventory.ini -a "src=/var/siege.csv dest=~/tmp" -C


### update
push both config and URL's

    ansible-playbook -M modules -i files/inventory.ini tasks/siege-update.yml -C

    
### reboot

    ansible siege -i files/inventory.ini -a "/sbin/reboot"

### TODO
    Update Documentation, roll into quick start format
