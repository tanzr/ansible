# Ping
sudo ansible -u iaas bgo -m ping

# Run shell command
sudo ansible -u iaas -a 'ps aux | grep puppet' -m shell dev01

# Update/create himlarcli
sudo ansible-playbook -e "hosts=bgo-login:bgo-master" lib/himlarcli.yaml

# Distribute SSH keys for local git
sudo ansible-playbook -e "hosts=bgo-admin" lib/git_access.yaml

# Deploy puppet code to admin
sudo ansible-playbook -e "hosts=bgo-admin" lib/deploy_himlar.yaml

# Toggle puppet run with action=[enable|disable]
sudo ansible-playbook -e "hosts=bgo action=enable" lib/toggle_puppet.yaml

# Shutdown all nodes on controller
sudo ansible-playbook -e "hosts=test01-controller-02 action=stop" lib/manage_nodes.yaml

# Push secret files (will need secret_files hash defined for host or group)
sudo ansible-playbook -e "hosts=local1-dashboard-01" lib/push_secrets.yaml

# Remove SSH hosts from .known_hosts on login
bin/ssh_clean.py local2-db
(wrapper pythton script to allow run on muliple hosts. All valid ansible groups
can be used)

# Update repo pointers (after changes have been commited to the repo-admin git repo)
sudo ansible-playbook -e "hosts=download" lib/update_repo.yaml
