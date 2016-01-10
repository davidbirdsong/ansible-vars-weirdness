##### Issue Type:

Can you help us out in labelling this by telling us what kind of ticket this this?  You can say:
  - Bug Report
 
##### Ansible Version:
 v2.0.0-0.9.rc4 from checkout

##### Ansible Configuration:

trying out ansible 2.0

##### Environment:
```sh
[david@sjc1-b4-8 ]$ cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=14.04
DISTRIB_CODENAME=trusty
DISTRIB_DESCRIPTION="Ubuntu 14.04.2 LTS"
```

##### Summary:

with `ANSIBLE_PRIVATE_ROLE_VARS=1` local variables to a role1 are not available to pass to another role2 where role2 is declared as a dependency to role1 

##### Steps To Reproduce:
checkout https://github.com/davidbirdsong/ansible-vars-weirdness
```sh
export ANSIBLE_PRIVATE_ROLE_VARS=1
ansible-playbook test.yml
```
##### Expected Results:

```
PLAY ***************************************************************************

TASK [setup] *******************************************************************
ok: [127.0.0.1]

TASK [reusablerole : test] *****************************************************
ok: [127.0.0.1] => {
    "msg": "value=testcommon_value_1_plus_tld_val"
}

TASK [toprole : check_job-vars] ************************************************
ok: [127.0.0.1] => {
    "msg": "tld_val=testcommon_value_1_plus_tld_val"
}

PLAY RECAP *********************************************************************
127.0.0.1                  : ok=3    changed=0    unreachable=0    failed=0   

```
##### Actual Results:
```
PLAY ***************************************************************************

TASK [setup] *******************************************************************
ok: [127.0.0.1]

TASK [reusablerole : test] *****************************************************
fatal: [127.0.0.1]: FAILED! => {"failed": true, "msg": "ERROR! ERROR! ERROR! 'testcommon' is undefined"}

PLAY RECAP *********************************************************************
127.0.0.1                  : ok=1    changed=0    unreachable=0    failed=1   

```

