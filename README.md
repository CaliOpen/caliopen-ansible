This is an ansible repository for deployment of Caliop POC

Only webtier managed at this time with a nginx using only HTTPS

Installation:
- make a virtualenv, activate it
- pip -r requirements.txt
- edit a hosts file with a webservers category and your target machine(s)
- ansible-playbook -i hosts webservers.yml


Known issues:
- install of npm failed at this time, do task manually

- python caliop package installation make things not working properly
  - task to uninstall and do a python setup.py develop exists to try to
  fix that point, may work not as expected

- grunt build task failed except if you have a chrome installed ...
  do it manually (be sure to be the project user). Remove karma tasks
  in Gruntfile.js to make it stop complain about $CHROME_BIN.

  SYMPTOM: pserve will complain about not found template in caliop.ng/bin directory

- certificate private key is git-crypted, replace roles/web/files/certs/ by your own
  and the related certificate
