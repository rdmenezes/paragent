# Introduction #

This is a guide for installing the Paragent agent msi on clients using Active Directory's Group Policy Object (GPO) system. Microsoft has many support articles detailing Active Directory. These instructions are adapted from http://support.microsoft.com/kb/816102.

### Locating the MSI File ###

First, we will need to create a distribution point from which client computers can download the Paragent MSI file.

  1. Log onto your server as an administrator
  1. Create a shared network folder where you will put the MSI file
  1. Set permissions on the share created in the previous step so that clients will have access to the MSI file
  1. Copy the Paragent agent MSI file to the share

### Create the Group Policy Object ###

Second, we need to create a GPO package to represent the Paragent Agent installation.

  1. Start the Active Directory Users and Computers snap-in. To do this, click **Start**, point to **Administrative Tools**, and then click **Active Directory Users and Computers**.
  1. In the console tree, right-click your domain, and then click **Properties**.
  1. Click the **Group Policy** tab, and then click **New**.
  1. Type a name for this new policy (for example, Paragent Agent), and then press ENTER.
  1. Click **Properties**, and then click the **Security** tab.
  1. Click to clear the **Apply Group Policy** check box for the security groups that you want to prevent from having this policy applied.
  1. Click to select the **Apply Group Policy** check box for the groups that you want this policy to apply to.
  1. When you are finished, click **OK**.

### Publish the Paragent Agent Package ###

Third, we need to assign the Paragent agent package to computers.

  1. Start the Active Directory Users and Computers snap-in. To do this, click **Start**, point to **Administrative Tools**, and then click **Active Directory Users and Computers**.
  1. In the console tree, right-click your domain, and then click **Properties**.
  1. Click the **Group Policy** tab, select the Paragent Agent group policy object, and then click **Edit**.
  1. Under **Computer Configuration**, expand **Software Settings**.
  1. Right-click **Software installation**, point to **New**, and then click **Package**.
  1. In the **Open** dialog box, type the full Universal Naming Convention (UNC) path of the shared installer package that you want. For example, \\file server\share\Paragent.msi. **Important** Do not use the Browse button to access the location. Make sure that you use the UNC path to the shared installer package.
  1. Click **Open**.
  1. Click **Assigned**, and then click **OK**. The package is listed in the right pane of the **Group Policy** window.
  1. Close the **Group Policy** snap-in, click **OK**, and then quit the Active Directory Users and Computers snap-in.
  1. When the client computer starts, the managed software package is automatically installed.

### Permissions ###

We have run into certain situations where the agent is listed in the Add/Remove programs group (under the name **Templar**), but there are no contents in the installation directory. This is the result of insufficient privileges on the client machine to perform the installation. To make sure your permissions are correct:

  1. Start the Active Directory Users and Computers snap-in. To do this, click **Start**, point to **Administrative Tools**, and then click **Active Directory Users and Computers**.
  1. In the console tree, right-click your domain, and then click **Properties**.
  1. Click the **Group Policy** tab, select the Paragent Agent group policy object, and then click **Edit**.
  1. When you are looking at your GPO object, drill down into **Computer Configuration > Administrative Templates > Windows Components > Windows Installer**.
  1. Enable the permission **Always install with elevated privileges**.
  1. The same option can also be set for the **User Configuration > Administrative Templates > Windows Components > Windows Installer** branch as well.

The following is a screenshot of the permission in question.

![http://paragent.googlecode.com/files/gpo-permissions-1.png](http://paragent.googlecode.com/files/gpo-permissions-1.png)