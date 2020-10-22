# GL_BaseCamp
Prerequisites
4 linux machines (VMs, instances in Digital Ocean, GCP, AWS EC2, dosen't matter);
Python installed (2.7 or 3.5+);
established password-less connection from one machine (controller) to others;
ps: one of machine (controller) can be a Windows 10 machine with WSL/WSL2

Task
Create a inventory file with four groups, each provisioning VM should be in separate group and group named iaas what should include childrens from two first groups;
Create reusable roles for that:
creating a empty file /etc/iaac with rigths 0500, this role should be idempodent
define content of /etc/issue as variable
Create playbook for:
invoke the role for /etc/iaac for hosts group iaas
invoke the role for defining variable for all hosts
print in registered variables
printing hostnames together with registered variables will be a plus.
Create a repo in your GitHub account and commit code above
Optional:

use ansible_user and ansible_password for ssh connection and store passwords for each VM in encrypred way (add vault password to README.md in this case)
***************************************************************************************************************************************************************************************

My Homework:

I have created 5 vms on vmware(1 ansible controller other 4vms it for test) and have created 4 host group / 2 roles / 1 playbook
***************************************************************************************************************************************************************************************

ansible-playbook playbook.yml


Result:
***************************************************************************************************************************************************************************************
[root@centos7-ansible-ctrl ansible]# ansible-playbook playbook.yml

PLAY [Create a empty file with 0500 permission] ***************************************************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************************************************************************************
ok: [centos7-test01]
ok: [centos7-test02]

TASK [creating_a_empty_file : Create a empty file.] ***********************************************************************************************************************************
changed: [centos7-test02]
changed: [centos7-test01]

PLAY [Define content as variable and printing hostnames] ******************************************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************************************************************************************
ok: [centos7-test03]
ok: [centos7-test04]

TASK [define_content : Print hostnames together with registered variables.] ***********************************************************************************************************
changed: [centos7-test01]
changed: [centos7-test04]
changed: [centos7-test02]
changed: [centos7-test03]

TASK [define_content : debug] *********************************************************************************************************************************************************
ok: [centos7-test03] => {
    "msg": "Hostname centos7-test03  have the 'path' variable value is \\S\nKernel \\r on an \\m"
}
ok: [centos7-test04] => {
    "msg": "Hostname centos7-test04  have the 'path' variable value is \\S\nKernel \\r on an \\m"
}
ok: [centos7-test01] => {
    "msg": "Hostname centos7-test01  have the 'path' variable value is \\S\nKernel \\r on an \\m"
}
ok: [centos7-test02] => {
    "msg": "Hostname centos7-test02  have the 'path' variable value is \\S\nKernel \\r on an \\m"
}

PLAY RECAP ****************************************************************************************************************************************************************************
centos7-test01             : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
centos7-test02             : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
centos7-test03             : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
centos7-test04             : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

***************************************************************************************************************************************************************************************

Result from first role:

[root@centos-test01 yg]# ll -al /etc/iaac
-r-x------. 1 root root 0 Oct 22 10:26 /etc/iaac

[root@centos7-test02 yg]# ll -al /etc/iaac
-r-x------. 1 root root 0 Oct 22 10:26 /etc/iaac
