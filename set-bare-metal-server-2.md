---

copyright:
  years: 2017, 2025
lastupdated: "2025-09-18"

keywords: set up bare metal server

subcollection: bare-metal

---

{{site.data.keyword.attribute-definition-list}}

# Setting up a bare metal server
{: #bm-set-up}

You can set up a Bare Metal Server as a dedicated server.
{: shortdesc}

## Before you begin
{: #bm-set-up-before}

* Go to your console's device menu.
* Make sure that you have any necessary account permissions and device access. Only the account owner, or a user with the **Manage users** classic infrastructure permission, can adjust the permissions.

For more information about permissions, see [Classic infrastructure permissions](/docs/account?topic=account-mngclassicinfra) and [Managing device access](/docs/virtual-servers?topic=virtual-servers-managing-device-access).

## Setting up a bare metal server
{: #bm-setting-up-server}

Use the following steps to set up a Bare Metal Server:

1. From the menu, click **Devices** > **Device list** and find your system. All of your devices are detailed in the Device List, where you can manage devices, upgrade devices, or generate bandwidth usage charts.
1. Choose to manage your server in one of the following ways:
   * Click the Device Name arrow to view a summary and manage your devices from the Snapshot view.
   * Click the Device Name of the server to view a detailed list and manage your devices from the Device Details screen.
1. Record the IP address and credentials for the server in a safe location so that you can access the details quickly without needing to log in each time you need them. You can record these details for both an individual device and for all devices that are associated with your account:
   * View individual device IPs from the Device List.
   * View individual device root passwords in the Snapshot View for the device.
   * View multiple device IPs by using the **Download CSV** option from the **Device List**. Then, select **Download CSV** from the **Settings** cog to download a full list of devices and details in spreadsheet format.
1. Update the credentials for operating systems and other software. All of the software that was loaded onto your device during the provisioning process was assigned temporary credentials. You can view and manage these credentials on the Passwords tab of each device in the {{site.data.keyword.cloud}} console. Use these temporary credentials to access your software for the first time. Then, change the password to your software by following strong password practices. Create a password that consists of a combination of letters, numbers, and symbols. Optionally, you can store password updates on the Passwords tab for each device. However, when you store passwords, any person with access to the account and appropriate permissions can view the passwords that are stored on the Passwords screen.
1. Access your server on the private network. You can use the {{site.data.keyword.cloud_notm}} infrastructure private network to interact with your devices through remote desktop (RDP) by using SSH and KVM over IP. You can use the VPN Access tool for private network connection to either the closest SSL VPN endpoint or to the endpoint of your choice. VPN access is also required to interact with several services. To access the private network, edit the user’s VPN access from the User List. To access the User List, click **Account** > **Users** > **User list**. Use the [Virtual Private Network](https://www.ibm.com/products/vpn-access){: external} page to connect to one of the various VPN options.
1. After you have your infrastructure and environments up and running, you are ready to set up your monitoring service. {{site.data.keyword.mon_full_notm}} gives you insight into the performance and health of your applications, services, and platforms. Your administrators, DevOps teams, and developers have a full-stack telemetry with advanced features to help them monitor and troubleshoot, define alerts, and design custom dashboards. For more information, see [{{site.data.keyword.mon_full_notm}}](/docs/?topic=monitoring-getting-started).
1. Secure your system. Use the available hardware firewalls to secure your device. You can provision hardware firewalls on demand with no downtime, if rules are established properly, to protect your server from unwanted activity. After you order your firewall, it must be enabled and rules must be set.
1. Schedule backups to make sure that your data is safely stored outside of your device and able to reload any lost data. You can choose from various backup services to store your data in a secure location:
   * {{site.data.keyword.cloud}} Backup is an automated, agent-based backup system. {{site.data.keyword.cloud}} Backup is a “set-and-forget” solution for managing your device. It is compatible with Microsoft software such as Exchange and SQL through extra plug-ins. {{site.data.keyword.cloud}} Backup users interact with this service through the {{site.data.keyword.cloud}} Backup WebCC web-based application.
   * R1Soft Continuous Data Protection (CDP) can be installed on your server or self-managed virtual machine. It is recommended if you are looking for a single interface to manage all of your backups. You interact with R1Soft CDP through your proprietary management system, which allows agents to be installed on virtual machines and offers database plug-ins for extra functions.
