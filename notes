Ansible Engine Support – Ansible Playbook

1.       Automate Account Creation

2.       Patching

3.       Implementing STIG

4.       Password Reset and Update

5.       Best Practices

·         Utilize GitLab – Link sent by Mr. Jean Figarella (Red Hat Consultant)

1.       https://software.af.mil/dsop/

2.       https://dccscr.dsop.io/users/sign_in

Contact: 
		"Ramos, Cyril L CIV USN FLEWEACEN SAN CA (USA)" <cyril.ramos@navy.mil>,
"Harkness, Danny R Jr CTR USMC MWHS-3 (USA)" <danny.harkness1@navy.mil>,
"Vanhouten, Jason J CTR (USA)" <jason.j.vanhouten1.ctr@navy.mil>

--------------------------------------------------------------------------------------

Created by Joshua Bister
Email: jbister@redhat.com

PREPARING PROJECT FOLDER
========================
mkdir project_folder
cd project_folder
python3 -m venv venv
source venv/bin/activate
pip install ansible
NOTE: we create the venv outside the roles folders so that the binaries are not uploaded to git

CREATE NEW ROLE
===============
ansible-galaxy role init role_name
vim role_name/meta/main.yml
vim role_name/README.md
cd role_name
git init ansible-role-role_name (follow a naming convention in git)
git add remote git@github.com:username/ansible-role-role_name remote_name
git branch DEV
git checkout -b feature_branch
git add .
git commit -m "Initial Commit"
git push origin 

CREATE NEW ROLE (ADVANCED)
=========================
pip install docker molecule
(instead of ansible-galaxy role init role_name) ->
molecule init role role_name -d docker

MODIFY ROLE
===========
vim role_name/tasks/main.yml
cd role_name
git add .
git commit -m "updated this logic"
git push origin feature_branch

INSTALL ROLE
===========
ansible-galaxy role install -r file_with_roles_config.yaml

UNINSTALL/DELETE ROLE
=====================
ansible-galaxy remove role_name (this will REMOVE the role from LOCAL MACHINE. delete will remove the role from Ansible Galaxy)

CALLING A PLAYBOOK
==================
ansible-playbook -i inventory example_multiple_roles_playbook.yml
