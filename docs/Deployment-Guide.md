- Deployment Guide
  - [Prerequisites](#prerequisites)
  - [Deployment Steps](#Deployment-Steps)
    - [Create a Team](#1-create-a-team)
    - [Import the Flows to Teams Dataverse](#2-import-the-flows-to-teams-dataverse)
    - [Create SharePoint List for image storage](#3-create-sharePoint-list-for-image-storage)
    - [Import the Admin app solution to Teams Dataverse](#4-import-admin-configuration-app)
    - [Configure Categories table with configuration app](#5-configure-categories-table-with-configuration-app)
    - [Import the Solution to Teams Dataverse](#6-import-the-helpDesk-app-to-teams-dataverse)
    - [Configuration Settings](#7-configuration-settings)
    - [Configuration optional cleanup Flow](#8-configure-cleanup-flow)
  - [Troubleshooting](#9-troubleshooting)

- - -

# Prerequisites

To begin, you will need:

- An Office 365 subscription where you can create the following kinds of resources:  
  - Teams
  - Power Apps
- A team with the users who will be submitting HelpDesk tickets with this app. (You can add or remove team members later!)
- A team for help desk app agents, members of this team will be able to view and manage tickets submitted by users. (You can add or remove team members later!)
- A copy of the HelpDesk app [GitHub repo] (https://github.com/FedSolutions/helpdesk/tree/main/Solution)

- - -

# Deployment Steps

## 1. Create a Team

It is highly recommended that a dedicated Team is created for the HelpDesk App. To create a Team, follow the guidance below.

1. Open [Teams](https://teams.microsoft.com)
2. Within Teams, select **Teams** from the side-rail.

![Select Teams](assets/Deploy-CreateATeam-1.png)

3. Select **Join or create a team**.

![Join or Create a Team](assets/Deploy-CreateATeam-2.png)

4. Select **Create team**.

![Create Team](assets/Deploy-CreateATeam-3.png)

5. From the **Create a team** splash screen, select **From scratch**. NOTE: You can use “From a group or team”, but for simplicity, this documentation will start from scratch.

![From scratch](assets/Deploy-CreateATeam-4.png)

6. From the **What kind of team will this be?** screen, select **Private**. NOTE: Private provides the owner of the Team will control over who will be able to access the HelpDesk app. This Team can be “Public” or “Org-wide” however, this should be determine by your governance.

![Provide Name and Description](assets/Deploy-CreateATeam-5.png)

7. Provide a **Team Name** and **Description**. Select **Create**.
Example:
**Team Name**: Help Desk
**Description**: A location for employees to submit their HelpDesk tickets.

![Provide Name and Description 2](assets/Deploy-CreateATeam-6.png)

![Creating the Team](assets/Deploy-CreateATeam-7.png)

8. Add members to Help Desk. Select **Add**.
NOTE: Add names, distribution list(s), or security group(s). You can always add/remove members later

![Add Members](assets/Deploy-CreateATeam-8.png)

9. Select **Close**.

![Close](assets/Deploy-CreateATeam-9.png)

10. Congratulations! Your Team is ready!

![Team is Ready](assets/Deploy-CreateATeam-10.png)

## 2. Import the Flows to Teams Dataverse

1. Download the solution from the FedSolutions repository here: [Microsoft FedSolutions Help Desk](https://github.com/FedSolutions/helpdesk/tree/main/Solution)

2. Extract the zip file in latest version of solution folder. It will contain the following files:

![Select App](assets/InstallationFiles.png)

2. From the side-rail, select **Power Apps**.
NOTE: if you do not see Power Apps in the side-rail, click on Apps and search for Power Apps. Click **Add** (or **Open** if previously added).

![Select App](assets/DeployApp-ImportApp-0.png)

3. From the **Build** tab, select the appropriate team and click **See All** link at bottom.

![Select App](assets/DeployApp-ImportApp-1A.png)

4. Clicking on the See all link will take you to following page where you can click on import button

![Import App](assets/DeployApp-ImportApp-4A.png)

6. From the Select a file pane, select **browse** and navigate to the location where you downloaded the solution in Step 1.

![Browse](assets/Deploy-ImportFlow-1.png)

7. Select **Next**.

8. On the **Import** pane, **verify only the following items are selected** and select **Import**.

![Next](assets/Deploy-ImportFlow-2.png)

10. Select and fix all connection references. Once new connection is created click on the refresh button and it should update connection reference. 

![Next](assets/Deploy-ImportFlow-3.png)

11. Click Ok and should take you to another screen and once Flows are imported you will see the following message

![Next](assets/Deploy-ImportFlow-4.png)
## 3. Create SharePoint list for image storage

There is a requirement to store images in SharePoint. This reduces the storage required in your Dataverse database. The following steps will help you create a list in SharePoint that can be used to store images.

  1. Open PowerApps within Teams, click on Build tab and select Team where Help Desk app is deployed. 
  2. Select Cloud Flows from left navigation
     ![SharePoint List Flow](assets/Deploy-SPList-1.png)
  3. Run the Flow called **CreateTicketAttachmentList**
     ![Run Flow](assets/Deploy-SPList-2.png)
  4. When prompted for SPOUrl enter the URL of SharePoint site where Help Desk app is deployed and click Run Flow. 
     ![Run Flow](assets/Deploy-SPList-3.png)
  5. Naviagte to the SharePoint site where Help Desk app is deployed and select view all site content and click on the **TicketAttachments** list. 
  6. Click on the gear icon on top right of the screen and select **List Settings**.  
     ![List Settings](assets/Deploy-SPList-4.png)
  7. Click on the **Advanced settings** link from the list settings page.
     ![Advanced List Settings](assets/Deploy-SPList-5.png)
  8. Update the item level security to the following settings and click OK. 
     ![Advanced List Settings](assets/Deploy-SPList-6.png)
## 4. Import Admin Configuration App

1. Download the admin app solution from the FedSolutions repository here: [Microsoft FedSolutions Help Desk](https://github.com/FedSolutions/helpdesk/tree/main/Solution)

2. From the side-rail, select **Power Apps**.
NOTE: if you do not see Power Apps in the side-rail, click on Apps and search for Power Apps. Click **Add** (or **Open** if previously added).

![Select App](assets/DeployApp-ImportApp-0.png)

3. From the **Build** tab, select the appropriate team and click **See All** link at bottom.

![Select App](assets/DeployApp-ImportApp-1A.png)

4. Clicking on the See all link will take you to following page where you can click on import button

![Import App](assets/DeployApp-ImportApp-4A.png)

6. From the Select a file pane, select **browse** and navigate to the location where you downloaded the solution in Step 1.

![Browse](assets/DeployConfigApp-1.png)

7. Select **Next**.

![Next](assets/DeployConfigApp-2.png)

8. Click on the **Import** button.

9. Select the HDManagementApp under the **Apps** tab.

10. Click on the Teams icon with PowerApp designer surface to publish the app to Teams.

![Next](assets/DeployConfigApp-3.png)

11. Select **Next**.

![Next](assets/DeployConfigApp-4.png)

12. Select the channel within the Team where the Help Desk App will be published and select **Save and Close**.

![General](assets/DeployConfigApp-5.png)
## 5. Configure categories table with configuration app.

The category table is used to configure the categories that will be used by the Help Desk app. Each category will allow you to setup an email address for the supporting team as well as the channel within a Team that messages will be posted when a user opens a ticket. The following steps will help you configure the categories table. Members of the Teams selected in the category table will be configured as agents in the Help Desk app. Agents will have ability to take action on tickets, close tickets and reassign tickets.

1. Open the HD Configuration App from within Teams and click on **New Record**.

![New Record](assets/Config-HDCategories-1.png)

2. Add a category name, then click on the search icon next to GroupID.

![New Record](assets/Config-HDCategories-2.png)

3. Select the group from the populate list.

![Select group](assets/Config-HDCategories-3.png)

4. Click on the search icon next to CategoryID.

5. Select the channelId from the popup window for that group.

![Select group](assets/Config-HDCategories-5.png)

6. Select active from the status, enter an email address for the HelpDesk or specific team that supports that category. Click on the save icon to save the record.

![Complete category](assets/Config-HDCategories-6.png)

7. Repeat steps 2-6 for each category you need to configure. 
## 6. Import the HelpDesk app to Teams Dataverse

1. Download the solution from the FedSolutions repository here: [Help Desk](https://github.com/FedSolutions/helpdesk/tree/main/Solution)

2. From the side-rail, select **Power Apps**.
NOTE: if you do not see Power Apps in the side-rail, click on Apps and search for Power Apps. Click **Add** (or **Open** if previously added).

![Select App](assets/DeployApp-ImportApp-0.png)

3. From the **Build** tab, select the appropriate team and click **See All** link at bottom.

![Select App](assets/DeployApp-ImportApp-1A.png)

- If no apps appear in list select the **Import your solution link**

![Import App](assets/DeployApp-ImportApp-1.png)

4. Clicking on the See all link will take you to following page where you can click on import button

![Import App](assets/DeployApp-ImportApp-4A.png)

6. From the Select a file pane, select **browse** and navigate to the location where you downloaded the solution in Step 1.

![Browse](assets/DeployApp-ImportApp-2.png)

7. Select **Next**.

![Next](assets/DeployApp-ImportApp-3.png)

8. On the **Import** pane, verify all items are selected and select **Import**.

![Importing 2](assets/DeployApp-ImportApp-4.png)

9. When the Import is complete, select apps from left menu and click on the Help Desk App. This will open application in PowerApps editor. You may be prompted to allow the data connections

![Importing 2](assets/Config-HelpDeskApp-1.png)

10. Update Ticket attachments data connection within the app. Select Data from left rail of PowerApps editor and remove ticketattachments data connection.

![Remove Connection](assets/Config-HelpDeskApp-2.png)

11. Click on add a connection under Data tab and select SharePoint.

![Add Connection](assets/Config-HelpDeskApp-3.png)

12. Enter url of SharePoint site where HelpDesk app is deployed and click on connect.

![Connect SharePoint site](assets/Config-HelpDeskApp-4.png)

13. Select TicketAttachment list and c

![Connect SharePoint site](assets/Config-HelpDeskApp-5.png)

10. Click on allow when prompted for connections and then publish to Team.

![Importing 2](assets/Config-HelpDeskApp-6.png)

![Importing 2](assets/Config-HelpDeskApp-7.png)

Select desired channel to publish app. Once publish is complete you should see Help Desk App and tab within channel.
## 7. Configuration Settings

There are configuration settings that need updated in order to run the Help Desk application. Setting up the deep linking is a manual process. The other configuration settings can be updated using the admin app.
### Configuring the deeplink value

In the HD_Ticket_Settings_01S table add a row for DeepLink in Teams. This is required for DeepLink from Teams post to ticket within the Help Desk application.

1. Create the deeplink value by copying the link from Teams under the published tab by selecting **copy link to tab**.

![Get link](assets/UpdateTable-DeepLink-1.png)

2. Paste the link in Notepad.

3. Replace the word null in url with value **%22TicketID%22** This value is case sensitive so make sure you are using the correct value.

4. Copy deeplink value from Notepad and update HD_Ticket_Settings_01S by opening table in PowerApps and updating the value.

![Get link](assets/UpdateTable-DeepLink-3.png)

If the value column is not visible click on the Add column button and select Value.

![Add column](assets/UpdateTable-DeepLink-4.png)

![Update values](assets/UpdateTable-DeepLink-2.png)

## 8. Configure cleanup Flow

This Flow is optional to deploy and designed to purge data from the Help Desk ticket and comments dataverse tables to conserve space. You may want to take a [backup](https://docs.microsoft.com/en-us/power-platform/admin/backup-restore-environments) or [export] old data prior to running this Flow. 

1. In the HD_Ticket_Settings_01S table add a row for PurgeDays. Enter the numbers of days of data you would like to keep in Help Desk application. The HelpDeskCleanup Flow is schedule to delete all tickets with a **Closed** status older than days specified in PurgeDays record.

![Add row](assets/UpdateTable-PurgeData-1.png)

2. Edit the HelpDeskCleanUp Flow and set the reoccurrence to desired schedule. You could also change this trigger to be manually invoked instead of scheduled.  

![Update Schedule](assets/UpdateTable-PurgeData-2.png)

3. To schedule the Flow make sure its turn on.

![Enable Flow](assets/UpdateTable-PurgeData-3.png)

## 9. Troubleshooting
