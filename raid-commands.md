---

copyright:
  years: 1994, 2024
lastupdated: "2024-09-13"


keywords: raid controller commands, raid commands

subcollection: bare-metal

---

{{site.data.keyword.attribute-definition-list}}

# RAID controller commands
{: #bm-raid-controller-commands}

You can use the Adapatec&reg; CLI to run RAID controller commands. The following commands are the most common RAID controller commands that you might use.
{: shortdesc}

`/usr/Adaptec_Event_Monitor/arcconf getstatus 1`

`_GETSTATUS_` lists the type of operation, logical drive number, logical drive size, and progress of the operation. You can also see the status of any background commands that are running, such as the following items:

* Most recent rebuild
* Synchronization
* Logical-drive migration
* Compaction/expansion

`/usr/Adaptec_Event_Monitor/arcconf getconfig 1`

`_GETCONFIG_` lists information about controllers, logical drives, and physical drives. You can see information such as the following items:

* Controller type
* BIOS, boot block, device driver, and firmware versions
* Physical device type, device ID, presence of PFA
* Physical device state
* Enclosure information: fan, power supply, and temperature

`/usr/Adaptec_Event_Monitor/arcconf getlogs 1 device tabular`

`_GETLOGS_` gives you access to the status and event logs of a controller. `_DEVICE xxx_` displays a log of any device errors that the controller encounters.

See the following example for output that is made by using the _GETLOGS_ command:

```text
driveErrorEntry
smartError.. ............................ false
vendorID ................................ WDC
serialNumber ............................ WD-XXX
wwn ..................................... xxxxxxxxxxxxxxxx - CC_FILTER
deviceID ................................ 10
productID ............................... WD1003FB
numParityErrors ......................... 0
linkFailures ............................ 0
hwErrors ................................ 0
abortedCmds ............................. 7
mediumErrors ............................ 20
smartWarning ............................ 0
```
{: codeblock}

`/opt/MegaRAID/storcli/storcli64 /c0/eall/sall show all | grep -iE "det|cou|tem|SN|S.M|fir”`

You use this command to show the specific drives and any possible drive errors that it might have.
The following example shows the output:

```text
Drive /c0/e252/s0 - Detailed Information:
Shield Counter = 0
Media Error Count = 0
Other Error Count = 0
Drive Temperature = 24C (75.20 F)
Predictive Failure Count = 0
S.M.A.R.T alert flagged by drive = No
SN = XXXX
Firmware Revision = SN04

Drive /c0/e252/s1 - Detailed Information:
Shield Counter = 0
Media Error Count = 0
Other Error Count = 0
Drive Temperature = 22C (71.60 F)
Predictive Failure Count = 0
S.M.A.R.T alert flagged by drive = No
SN = xxxx
Firmware Revision = SN03

Drive /c0/e252/s2 - Detailed Information:
Shield Counter = 0
Media Error Count = 0
Other Error Count = 0
Drive Temperature = 21C (69.80 F)
Predictive Failure Count = 0
S.M.A.R.T alert flagged by drive = No
SN = xxxx
Firmware Revision = SN04

Drive /c0/e252/s3 - Detailed Information:
Shield Counter = 0
Media Error Count = 0
Other Error Count =
Drive Temperature = 23C (73.40 F)
Predictive Failure Count = 0
S.M.A.R.T alert flagged by drive = No
SN = xxxx
Firmware Revision = SN03
```
{: codeblock}

`/opt/MegaRAID/storcli/storcli64 /c0/eall/sall show rebuild`

This command displays the rebuild status of all drives and the estimated time to complete the rebuild. You see this output when you run the command:

```text
---------------------------------------------
Drive-ID Progress% Status Estimated Time Left
---------------------------------------------
/c0/e252/s0 - Not in progress
/c0/e252/s1 - Not in progress
/c0/e252/s2 - Not in progress
/c0/e252/s3 - Not in progress
---------------------------------------------
```
{: codeblock}

`RAID alert "Spam"`

Change the "global" section of the default config (`/opt/Broadcom/mrmonitor/MegaMonitor/config-current.xml`):

```text
<global>
<severity level="FATAL">
<do-systemlog/>
<do-email/>
</severity>
<severity level="CRITICAL">
<do-email/>
<do-systemlog/>
</severity>
<severity level="WARNING">
<do-email/>
<do-systemlog/>
</severity>
<severity level="INFO"><do-systemlog/>
</severity>
</global>
```
{: codeblock}

To read like this:

```text
<global>
<severity level="FATAL">
<do-systemlog/>
<do-email/>
</severity>
<severity level="CRITICAL">
<do-email/>
<do-systemlog/>
</severity>
<severity level="WARNING">
<do-systemlog/>
</severity>
<severity level="INFO">
<do-systemlog/>
</severity>
</global>
```
{: codeblock}

Remove the "do-email" tag for level "WARNING". Alternatively, change the security level to "INFO".
{: note}

## Common drive errors
{: #bm-common-drive-errors}

The most common driver errors are smart errors, hardware errors, and medium errors. You see these errors if a drive is failing. So, you need to replace the drive as soon as possible.

Although not unusual, aborted commands are another common error. But, if aborted commands increase in number (such as 100), open a support case.

Link errors can indicate that a cable might need reseated or replaced.

### Support case information
{: #bm-raid-support}

The following information is needed when you open support case.

#### Adaptec RAID cards
{: #adaptec-raid-cards-support}

Make sure that you include the full output of `arcconf getconfig 1/arcconf getlogs 1 device tabular` when you open a support case. Providing this information helps the support team identify drive order, array membership, array geometry, and cabling issues. This information is critical to the recovery of a lost RAID configuration. Granting permission to restart/power down in the initial update or asking it to be hot-swapped speeds up the support case process.

#### Broadcom RAID cards
{: #broadcom-raid-cards-support}

Use the following commands to obtain the log files for Broadcom RAID cards. You need to include the full output of these log files with your support case.
```text
/opt/MegaRAID/storcli/storcli64 /c0 show all
/opt/MegaRAID/storcli/storcli64 /c0 show TermLog
/opt/MegaRAID/storcli/storcli64 /c0 /eall /sall show all | grep -iE "det|cou|tem|SN|S.M|fir"
/opt/MegaRAID/storcli/storcli64 /c0 show TermLog
```
{: codeblock}

#### Installing Storcli
{: #installing-storcli}

Use the following steps for Linux.

1) SSH into your server
2) `cd /tmp` (Or any directory you demand)
3) wget `http://downloads.service.softlayer.com/lsitools/1.14.12_StorCLI.zip`
4) Extract x.xx.xx_StorCLI.zip
5) cd `/tmp/storcli_all_os/Linux/` (or go to the downloaded directory)
6) rpm `-ivh storcli-x.xx.xx-x.noarch.rpm`
7) Check if storcli successfully installed

Use the following steps for Vmware ESXi.

1) Go to your /tmp directory.

   `# cd /tmp `

2) Download the storcli.

   `# wget http://downloads.service.softlayer.com/lsitools/1.14.12_StorCLI.zip`

3) Uncompress the file.

   `# unzip 1.14.12_StorCLI.zip'

4) Go to /tmp/storcli_all_os/Vmware-NDS/.

   `# cd /tmp/storcli_all_os/Vmware-NDS/'

5) Install the storcli.

   `# esxcli software vib install -v=/tmp/storcli_all_os/Vmware-NDS/vmware-esx-storcli-1.14.12.vib --no-sig-check`

After the storcli is installed, you can run these two commands to confirm the disk health of the server.

For ESXi 7.X, use the following commands.

   ```text
   /opt/lsi/storcli64/storcli64 /c0 show all
   /opt/lsi/storcli64/storcli64 /c0 show eventloginfo
   /opt/lsi/storcli64/storcli64 /c0 /eall /sall show all | grep -iE "det|cou|tem|SN|S.M|fir"
   /opt/lsi/storcli64/storcli64 /c0 show TermLog
   ```
   {: codeblock}

#### Check the RAID configuration
{: #check-raid-configuration}

Use the following commands to check the RAID configuration.

   ```text
   /opt/lsi/storcli64/storcli64 /c0 show all
   /opt/MegaRAID/storcli/storcli64 /c0 /eall /sall show all
   ```
   {: codeblock}

From the output, look for the topology section where the RAID type is listed as a column.

Make sure that you back up any work before you troubleshoot.
{: important}
