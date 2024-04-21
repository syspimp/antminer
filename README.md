# ansible antminer simple playbook
## What

simple playbook to reboot antminer when it is too hot and not mining

* tested on antminer s9k

## Why

I needed to reboot my bitcoin minner when it got too hot. I'm releasing this to share with you! This is for you!

## How
* run without tags to check status and display if the playbook would have reboot device
* run with "--tags report" to report/print antminer status and kernel log
* run with "--tags status" to report/print antminer status
* run with "--tags kernel" to report/print antminer kernel log
* run with "--tags reboot\_when\_hot" to reboot device during playbook run
* antminer checks the temperature every 30 minutes, so a cron running every 30 mins is sufficient

```
[user@lab ~]# crontab -l
30,0 * * * * /usr/bin/ansible-playbook --tags reboot_when_hot /home/user/check-miner.yml
[user@lab ~]# ansible-playbook --tags reboot_when_hot ./check-miner.yml 
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [localhost] *****************************************************************************************************************************************************************************************************************************

TASK [check antminer status] *****************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [transform status] **********************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [grab ghs rate] *************************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [report hash rate (ghs) average] ********************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "ghsav": "13675.7"
}

TASK [Get Miner Kernel Log] ******************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [reboot miner if temperature too high and ghs is zero] **********************************************************************************************************************************************************************************
skipping: [localhost]

TASK [Rebooting miner] ***********************************************************************************************************************************************************************************************************************
skipping: [localhost]

PLAY RECAP ***********************************************************************************************************************************************************************************************************************************
localhost                  : ok=5    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
 
```
