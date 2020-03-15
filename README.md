Ansible Engine Support – Ansible Playbook

1.       Automate Account Creation

2.       Patching

3.       Implementing STIG

4.       Password Reset and Update

5.       Best Practices

·         Utilize GitLab – Link sent by Mr. Jean Figarella (Red Hat Consultant)

--------------------------------------------------------------------------------------

Created by Joshua Bister
Email: jbister@redhat.com

PREPARING PROJECT FOLDER
========================
# Here we create a new folder, a python 3 virtual environment (venv), activate the venv, use pip to install ansible in the venv


mkdir project_folder  
cd project_folder  
python3 -m venv venv  
source venv/bin/activate  
pip install ansible  
NOTE: we create the venv outside the roles folders so that the binaries are not uploaded to git

CREATE NEW ROLE
===============
# Create a blank role template using ansible-galaxy (Remember to edit the meta and README!), create a git remote that points to our github repository, then commit and push the role to the repository. 
# Note that when using GitHub you must create the repository using a web browser in advance


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
# If you get a chance, I highly recommend checking out Molecule:
# https://molecule.readthedocs.io/en/latest/
# It may seem difficult at first, but it will double your development speed of ansible modules and make them more reliable due to testing!


pip install docker molecule  
(instead of ansible-galaxy role init role_name) ->  
molecule init role role_name -d docker  

MODIFY ROLE
===========
# tasks/main.yml is where the base logic of the ansible role happens, so this is a good place to start writing code.
# Remember to push to the repository when you've written working code. 
# It's a good idea to push periodically and/or whenever you get your code to a point that it works.
# Don't just push to DEV! Push to a feature branch and have a teammate review it and then you can both sign off on merging it into the DEV branch.


vim role_name/tasks/main.yml  
cd role_name  
git add .  
git commit -m "updated this logic"  
git push origin feature_branch  

INSTALL ROLE
===========
# See the file\_with\_roles\_config.yml in the top level directory
# This will install any role specified in the file.
# These will typically be URLs

ansible-galaxy role install -r file_with_roles_config.yaml


UNINSTALL/DELETE ROLE
=====================
ansible-galaxy remove role_name (this will REMOVE the role from LOCAL MACHINE. delete will remove the role from Ansible Galaxy)

CALLING A PLAYBOOK
==================
ansible-playbook -i inventory example_multiple_roles_playbook.yml

------------------------

GETTING THE STIG ROLE
=========================
# I'd highly recommend using the mindpoint group's version of the Red Hat STIG ansible role. See the example below for the URL.
# Either way the following steps work for both repositories:

# Create a new repository in your version control server then change the remote of the STIG folder you download
# Once that's done you can push the code to your own server and make changes to it to fit the needs of your organization

git clone https://github.com/MindPointGroup/RHEL7-STIG.git  
git checkout -b my\_dev\_branch
git remote set-url origin https://my-org-repository.url/username/repository\_name
git add .
git commit -m "Initial Commit"
git push origin master

RUNNING STIG AGAINST MY MACHINES
================================
# I'm not going to include a copy of the STIGS in my repository because having embedded repositories is a bad idea, 
# but I do include an example playbook that I might use to call the Mindpoint Group RHEL7-STIG role against some new servers

ansible-playbook -i inventory example\_stig\_playbook.yml


