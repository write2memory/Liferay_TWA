# Liferay_TWA
#Building a Custom Plant Care Tracker
Using Liferay [Objects](https://learn.liferay.com/w/dxp/low-code/objects), [Picklists](https://learn.liferay.com/w/dxp/low-code/objects/picklists), and [Forms](https://learn.liferay.com/w/dxp/low-code/forms/creating-and-managing-forms/creating-forms), you can keep track of all your plants, watering, and health status with a Custom Plant Care Tracker. 

To build a Custom Plant Care Tracker, you will [create two Picklists](https://learn.liferay.com/w/dxp/low-code/objects/picklists/creating-picklists?p_l_back_url=%2Flearn-search%3Fq%3Dcreate%2Bpicklist&p_l_back_url_title=Learn+Search&highlight=create%20picklist) and configure them in the Liferay Portal. The Picklists enforce standardized data entry for fields like Plant Health and Enviornment, preventing inconsistent data and making the dashboard easier to filter. Next, you will [create two Objects](https://learn.liferay.com/w/dxp/low-code/objects/creating-and-managing-objects/creating-objects) to store each plant’s profile and care logs that share relational data. Separating the plant profile and care logs allows users to track watering scheduled and health trends over time for each individual plant.  

![Custom Plant Care Tracker](/images/MyGarden_Dashboard.png)

[[TOC]]

##Prerequisites
To complete the step-by-step procedure in this article, please review and verify the following requirements: 

* A hosting environment with a minimum allocation of 8GB of available RAM
* A running instance of **Liferay Portal 7.4 CE (*GA100+*)** by [Installing a Liferay Tomcat Bundle](https://learn.liferay.com/w/dxp/self-hosted-installation-and-upgrades/installing-liferay-on-a-local-server/installing-a-liferay-tomcat-bundle) and [Configuring a Database](https://learn.liferay.com/w/dxp/self-hosted-installation-and-upgrades/installing-liferay-on-a-local-server/configuring-a-database)
* **Administrative access** to the Global Menu in the Liferay portal 

Start a new Liferay Portal CE instance by running the following command in your terminal: 

```bash
docker run -it -m 8g -p 8080:8080 liferay/portal:7.4.3.129-ga129
```

Sign in to Liferay at [http://localhost:8080](http://localhost:8080) using the email address ‘test@liferay.com’ and the password ‘test’. When prompted, change the password. 

##Adding an Environment Picklist
The first step is to create two separate Objects to manage your data sets. The Plant Object stores core plant details, while the related Care Log Object tracks the ongoing health and watering history for each plant.

1. Open the *Global Menu* (![Global Menu icon](/images/Global_Menu_icon.png)), go to the *Control Panel* tab, and click **Picklists**.

2. Click *Add* (![Add icon](/images/Add_icon.png)), enter ‘*Environment*’ for name, and then click **Save**. 

3. Select the new Picklist and use the Add button (![Add icon](/images/Add_icon.png)) to add the following items: 

| Name | Key |
| :--- | :--- |
| Indoor | Indoor |
| Outdoor | Outdoor |
| Seasonal Hybrid | Seasonal Hybrid |

[!Environment Picklist Items](/images/Environment_Picklist_Items.png) 

You can now use the Environment Picklist as a field in the Plant Object.

##Adding a Plant Health Picklist
Next, configure the **Plant Health Picklist** to enforce standardized data entry for health assessments.
Once created, this picklist is mapped to a field in the **Care Log Object**, ensuring that health status logs
remain consistent across all plant entries.

1. Open the *Global Menu* (![Global Menu icon](/images/Global_Menu_icon.png)), go to the *Control Panel* tab, and click **Picklists**.

2. Click *Add* (![Add icon](/images/Add_icon.png)), enter ‘*Plant Health*’ for name, and then click **Save**.

3. Select the new Picklist and use the Add button (![Add icon](/images/Add_icon.png)) to add the following items:

| Name | Key |
| :--- | :--- |
| Thriving | Thriving |
| Struggling | Struggling |
| Dormant | Dormant |

[!Plant Health Picklist Items](/images/Plant_Health_PicklistItems.png)

You can now use the Plant Health Picklist as a field in the Care Log Object.

Adding a Plant Object
The Plant Object stores the core attributes for each individual plant entry in the data set. As the parent
entity in a one-to-many relationship, it provides the foundation for linking recurring care activities to
individual records.

1. Open the *Global Menu* (![Global Menu icon](/images/Global_Menu_icon.png)), go to the *Control Panel* tab, and click **Objects**.

2. Click *Add* (![Global Menu icon](/images/Add_icon.png)) and enter the following values:

| Field | Value |
| :--- | :--- |
| Label | Plant |
| Plural Lable | Plants |
| Object Name | Plant |

3. Select the *Object*, click the *Fields* tab, and add the following fields:

| Label | Field Name | Type | Picklist | Required |
| :--- | :--- | :--- | :--- | :---: | 
| Common Name | commonName | Text | n/a | ✓ |
| Date Acquired | dateAcquired | Date | n/a | ✓ |
| Environment | environment | Picklist | Environment | ✓ | 
| Plant Photo | plantPhoto | Attachment | n/a | ✓ | 
| Is Toxic to Pets | isToxicToPets | Boolean | n/a | ✓ |

[!Plant Object Fields](/images/Plant_Object_Fields.png)

==NOTE: The Plant Object fields are customizable and are fully extensible beyond the data
attributes described in this article.==
