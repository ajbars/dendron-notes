---
id: hje384f0o1mr53e0z6ngo5i
title: Worknotes
desc: ''
updated: 1718032787608
created: 1717511047572
---
Curl with usage of netrc:

            sudo curl --netrc-file ~/.netrc -v -H -L -c cookies.txt -b cookies.txt -o vjw_script.py "https://github.adx.fcagroup.com/raw/tad/infra/master/ci/jenkins/pipelines/spin-up-vm/vjw_script.py" 


TODO: 
create a persistent folder in Jenkins pipeline
create a function to rsync back if you got stuff in the persistent_dir
figure out how to do the sync periodic in the best way
figure out how to do it in a dedicated terminal and how to do the last rsync when closing the terminal
cd into the working dir right after the ssh connection