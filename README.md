# Accelerator for PRM - Unmanaged Package Installation Instructions


Last Updated: March 16, 2023


## Pre-Installation Steps:

## These steps must be completed before installing the unmanaged package (Estimated time: 10 minutes)

1. **Ensure the following licenses are installed in your Salesforce org:**
    1. Health Cloud Sales - Enterprise Edition
    2. Salesforce Maps
    3. To confirm which licenses are installed in your org, please refer to this Help Article: [_https://help.salesforce.com/s/articleView?id=sf.distribution_assigning_user_licenses.htm&type=5_](https://help.salesforce.com/s/articleView?id=sf.distribution_assigning_user_licenses.htm&type=5) 
2. **Enable “Send Email” and Allow Activities**
    1. Setup > Search for “Deliverability”
    2. Select “Deliverability” 
    3. Set Send Email Access to “All Email”
    4. Refer to this Help Article for more information: [_https://help.salesforce.com/s/articleView?id=sf.data_sandbox_email_deliverability.htm&type=5_](https://help.salesforce.com/s/articleView?id=sf.data_sandbox_email_deliverability.htm&type=5) 
3. **Set the Organization-Wide Email Address**
    1. Setup > Email > Organization-Wide Addresses
    2. Add a new User Selectable Organization-Wide Email Addresses and choose a Display Name of your choosing.
    3. Verify the email address set by opening the link sent to the email address. 
4. **Enable Email-to-Case** 
    1. Setup a Default User if one is not already specified in your settings. 
    2. Turn on Email-To-Case.
    3. Refer to this Help Article for step-by-step instructions: [_https://help.salesforce.com/s/articleView?id=sf.customizesupport_enabling_email_to_case.htm&language=en_US_](https://help.salesforce.com/s/articleView?id=sf.customizesupport_enabling_email_to_case.htm&language=en_US&r=https%3A%2F%2Fwww.google.com%2F&type=5#:~:text=From%20Setup%2C%20enter%20Email%2Dto,%2DCase%2C%20and%20click%20Save)



## Installation Steps:

## These steps must be completed to install the unmanaged package of pre-built components for PRM

1. Navigate to the following website and complete the Download Now workflow: [_https://hlsaccelerators.developer.salesforce.com/s/bundle/a9E5f000000PKvwEAG/solution-accelerator-for-provider-relationship-management_](https://hlsaccelerators.developer.salesforce.com/s/bundle/a9E5f000000PKvwEAG/solution-accelerator-for-provider-relationship-management) 
    1. You will be prompted to acknowledge the Terms of Service, after which please enter your email address to receive a one-time confirmation code.
    2. Enter the confirmation code in the next step. After entering the code, you will have a chance to open these same instructions in your browser. 
    3. On the final step, you will be presented with “Install In My Org” which will bring you to the Salesforce login screen. Enter your credentials for the org in which you wish to install the accelerator. 
    4. Choose “Install for all users” when prompted. The installation process may take a few minutes. You will receive an email with installation confirmation when completed.
    5. If you have any issues with installation, please contact the HLS Accelerator team at [_lchristenbury@salesforce.com_](mailto:lchristenbury@salesforce.com). 

## Post-Installation Steps:

## These steps must be completed to enable the included components (Estimated Time: 1-2 hours)

**Enable Path to support the visual Path flow on the Case Lightning Record Page**


1. Follow these steps to enable the Path: [_https://help.salesforce.com/s/articleView?id=sf.path_enable.htm&type=5_](https://help.salesforce.com/s/articleView?id=sf.path_enable.htm&type=5)


**Configure Salesforce Maps**


1. Please follow these steps to set up Salesforce Maps: [_https://help.salesforce.com/s/articleView?id=sf.salesforce_maps_setup_maps.htm&type=5_](https://help.salesforce.com/s/articleView?id=sf.salesforce_maps_setup_maps.htm&type=5)
2. The package contains predefined custom fields for the Check-In Activity Fields. Please follow the steps in this Help Article: [_https://help.salesforce.com/s/articleView?id=sf.salesforce_maps_setup_check_in_activity_fields_select.htm&type=5_](https://help.salesforce.com/s/articleView?id=sf.salesforce_maps_setup_check_in_activity_fields_select.htm&type=5)
3. At the bottom of the Activity Settings, click “Suggest” to auto-assign the custom fields.
4. In the Field Set dropdown in Activity Settings, Select the Field Set “Salesforce Maps Check Out”.

![](/images/prm1.png)

**Configure Recommendation Record -** This Recommendation will show as a Next Best Action to your liaisons as they review contact records in Salesforce. If the custom field “Enrolled in Provider Portal?” on the Contact Record is Unchecked, then this recommendation will show.


1. Download the recommendation_1.csv file in the GitHub repository here: https://github.com/salesforce/Accelerator-for-Provider-Relationship-Management
2. Use DataLoader to import the Recommendation into your Salesforce org. 


**Meeting Reminder Flow and Email Template** 

1. This will enable the system to automatically send prospects or contacts an email reminder of an upcoming meeting 1 day before the meeting date. This helps decrease the no-show rate of prospects or contacts of liaison meetings.
2. Create a new Auto-Launched Flow titled “Meeting Reminder”
3. Configure the Flow Start as outlined below:
    1. Object: Event
    2. Trigger the Flow When: A record is created or updated
    3. Entry Conditions:
    4. Condition Requirements: Formula Evaluates to True
    5. Formula: {!$Record.ActivityDate} > TODAY()
    6. When to Run the Flow for Updated Records: Only when a record is updated to meet the condition requirements. 

![](/images/prm2.png)

1. On the Flow path, Click to add a Schedule Trigger:
    1. Set the Schedule Path to be “1 Day Before Event: Date”
    2. Time Source: Event: Due Date Only
    3. Offset Number: 1
    4. Offset Options: Day Before

![](/images/prm3.png)

1. Add a Flow Action of the following type: Email Alert
    1. Type = Email Alert
    2. Description = Meeting Reminder
    3. Email Template = the Email template record of your choosing. For additional information on how to create an email template, refer to this Help Article: [_https://help.salesforce.com/s/articleView?id=sf.email_create_a_template.htm&type=5_](https://help.salesforce.com/s/articleView?id=sf.email_create_a_template.htm&type=5) 
    4. Selected Recipients = Attendees
    5. From Email Address = Select the appropriate from email address according to your organization’s preferences.
2. Save and Debug your Flow to validate that it meets your business requirements
3. Once you are satisfied with the Flow, Activate the Flow. 


**Add “Confirm Meeting” Quick Action to your users’ Publisher Layout**

1. The package contains a Quick Action labeled “Confirm Meeting” which enables your Physician Liaison user to send a templated email to a contact/lead to confirm an upcoming meeting in one click. 
2. To enable this Quick Action, add the Quick Action to the active Publisher Layout assigned to the Physician Liaison Profile, or your Global Publisher Layout. 
3. Refer to this Help Article for more information on how to edit a Publisher Layout: [_https://help.salesforce.com/s/articleView?id=sf.working_with_global_publisher_layouts.htm&type=5_](https://help.salesforce.com/s/articleView?id=sf.working_with_global_publisher_layouts.htm&type=5) 

**Create a Physician Liaison Profile**

1. Navigate to Setup > Profiles > New Profile
2. Ensure the Profile is aligned to the Salesforce License Type
3. Name the Profile “Physician Liaison”
4. Ensure to align the Profile to these components:




![](/images/prm4.png)



## Unmanaged Package Component Inventory




| <br>Resources:                 |                                                                 |                       |                                      |                                    |
| ------------------------------ | --------------------------------------------------------------- | --------------------- | ------------------------------------ | ---------------------------------- |
| <br>**Action**                 | <br>**Component Name**                                          | <br>**Parent Object** | <br>**Component Type**               | <br>**Installation Notes**         |
| <br>Create                     | <br>NewEventPRM                                                 | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Account Layout - PRM                                        | <br>Account           | <br>Page Layout                      | <br>This is a brand new component. |
| <br>Create                     | <br>NewCasePRM                                                  | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>SendEmailPRM                                                | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>My Accounts Without Recent Activity                         |                       | <br>Report                           | <br>This is a brand new component. |
| <br>Create                     | <br>Task.Defer_Change_Date                                      | <br>Task              | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Screen_Shot_20220215_at_45040_PM1                           |                       | <br>Asset File                       | <br>This is a brand new component. |
| <br>Create                     | <br>Account Request                                             | <br>Case              | <br>Page Layout                      | <br>This is a brand new component. |
| <br>Create                     | <br>NewNotePRM                                                  | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Physician Liaison Performance Dashboard                     |                       | <br>Dashboard                        | <br>This is a brand new component. |
| <br>Create                     | <br>Account_Request_Path                                        |                       | <br>Path Assistant                   | <br>This is a brand new component. |
| <br>Create                     | <br>Provider                                                    | <br>Lead              | <br>Business Process                 | <br>This is a brand new component. |
| <br>Create                     | <br>My Check Ins                                                |                       | <br>Report                           | <br>This is a brand new component. |
| <br>Create                     | <br>Simple Task                                                 | <br>Task              | <br>Page Layout                      | <br>This is a brand new component. |
| <br>Create                     | <br>SampleHealthcarePractitionerFacilityContactConfigurationPRM |                       | <br>UI Object Relation Configuration | <br>This is a brand new component. |
| <br>Create                     | <br>Provider                                                    | <br>Lead              | <br>Record Type                      | <br>This is a brand new component. |
| <br>Create                     | <br>Provider                                                    | <br>Lead              | <br>Page Layout                      | <br>This is a brand new component. |
| <br>Create                     | <br>Confirm Meeting                                             | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Account Request                                             | <br>Case              | <br>Business Process                 | <br>This is a brand new component. |
| <br>Create                     | <br>My Completed Activities                                     |                       | <br>Report                           | <br>This is a brand new component. |
| <br>Create                     | <br>Liaison Reports                                             |                       | <br>Report Folder                    | <br>This is a brand new component. |
| <br>Create                     | <br>Physician Liaison Layout                                    | <br>Account           | <br>Compact Layout                   | <br>This is a brand new component. |
| <br>Create                     | <br>Case.SendEmailCase                                          | <br>Case              | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Enroll in Provider Portal                                   | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Physician Liaison Layout                                    | <br>Contact           | <br>Compact Layout                   | <br>This is a brand new component. |
| <br>Create                     | <br>LogACallPRM                                                 | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Simple Task                                                 | <br>Task              | <br>Record Type                      | <br>This is a brand new component. |
| <br>Create                     | <br>My Avg Check-In Distance from Account (f                    |                       | <br>Report                           | <br>This is a brand new component. |
| <br>Create                     | <br>NewTaskPRM                                                  | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Physician Layout PRM                                        | <br>Contact           | <br>Page Layout                      | <br>This is a brand new component. |
| <br>Create                     | <br>Salesforce Maps Check Out                                   | <br>Task              | <br>Field Set                        | <br>This is a brand new component. |
| <br>Create                     | <br>Referral Trend Report                                       |                       | <br>Report                           | <br>This is a brand new component. |
| <br>Create                     | <br>NewOpportunityPRM                                           | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Task.UpdatePriority_PRM                                     | <br>Task              | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>General                                                     | <br>Task              | <br>Record Type                      | <br>This is a brand new component. |
| <br>Create                     | <br>My New Leads                                                | <br>Lead              | <br>List View                        | <br>This is a brand new component. |
| <br>Create                     | <br>NewContactPRM                                               | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Account Request                                             | <br>Case              | <br>Record Type                      | <br>This is a brand new component. |
| <br>Create                     | <br>My Meeting Quality                                          |                       | <br>Report                           | <br>This is a brand new component. |
| <br>Create                     | <br>My Time Spent On Site                                       |                       | <br>Report                           | <br>This is a brand new component. |
| <br>Create                     | <br>SampleHealthcarePractitionerFacilityAccountConfigurationPRM |                       | <br>UI Object Relation Configuration | <br>This is a brand new component. |
| <br>Create                     | <br>Physician Liaison Layout                                    | <br>Lead              | <br>Compact Layout                   | <br>This is a brand new component. |
| <br>Create                     | <br>Liaison Dashboards                                          |                       | <br>Dashboard Folder                 | <br>This is a brand new component. |
| <br>Create                     | <br>New_Task_PRM                                                | <br>Global            | <br>Action                           | <br>This is a brand new component. |
| <br>Create                     | <br>Task.UpdateStatusPRM                                        | <br>Task              | <br>Action                           | <br>This is a brand new component. |
|                                |                                                                 |                       |                                      |                                    |
| <br>Apps:                      |                                                                 |                       |                                      |                                    |
| <br>**Action**                 | <br>**Component Name**                                          | <br>**Parent Object** | <br>**Component Type**               | <br>**Installation Notes**         |
| <br>Create                     | <br>Physician Relationship Management                           |                       | <br>App                              | <br>This is a brand new component. |
|                                |                                                                 |                       |                                      |                                    |
| <br>Flows:                     |                                                                 |                       |                                      |                                    |
| <br>**Action**                 | <br>**Component Name**                                          | <br>**Parent Object** | <br>**Component Type**               | <br>**Installation Notes**         |
| <br>Create                     | <br>Reminder to Enroll in Provider Portal                       |                       | <br>Flow Version                     | <br>This is a brand new component. |
|                                |                                                                 |                       |                                      |                                    |
| <br>Fields:                    |                                                                 |                       |                                      |                                    |
| <br>**Action**                 | <br>**Component Name**                                          | <br>**Parent Object** | <br>**Component Type**               | <br>**Installation Notes**         |
| <br>Create                     | <br>Check Out Distance From Record (mi)                         | <br>Activity          | <br>Custom Field                     | <br>This is a brand new component. |
| <br>Create                     | <br>Check Out Date/Time                                         | <br>Activity          | <br>Custom Field                     | <br>This is a brand new component. |
| <br>Create                     | <br>Meeting Quality                                             | <br>Activity          | <br>Custom Field                     | <br>This is a brand new component. |
| <br>Create                     | <br>Check In Date/Time                                          | <br>Activity          | <br>Custom Field                     | <br>This is a brand new component. |
| <br>Create                     | <br>Enrolled in Provider Portal?                                | <br>Contact           | <br>Custom Field                     | <br>This is a brand new component. |
| <br>Create                     | <br>Time on Site Minutes                                        | <br>Activity          | <br>Custom Field                     | <br>This is a brand new component. |
| <br>Create                     | <br>Days Since Last Visit                                       | <br>Account           | <br>Custom Field                     | <br>This is a brand new component. |
| <br>Create                     | <br>Check Out Date                                              | <br>Activity          | <br>Custom Field                     | <br>This is a brand new component. |
|                                |                                                                 |                       |                                      |                                    |
| <br>Recommendation Strategies: |                                                                 |                       |                                      |                                    |
| <br>**Action**                 | <br>**Component Name**                                          | <br>**Parent Object** | <br>**Component Type**               | <br>**Installation Notes**         |
| <br>Create                     | <br>Referring Providers                                         |                       | <br>Recommendation Strategy          | <br>This is a brand new component. |
|                                |                                                                 |                       |                                      |                                    |
| <br>Pages:                     |                                                                 |                       |                                      |                                    |
| <br>**Action**                 | <br>**Component Name**                                          | <br>**Parent Object** | <br>**Component Type**               | <br>**Installation Notes**         |
| <br>Create                     | <br>Physician_Relationship_Management_UtilityBar                |                       | <br>Lightning Page                   | <br>This is a brand new component. |
| <br>Create                     | <br>Lead_Record_Page_PRM                                        |                       | <br>Lightning Page                   | <br>This is a brand new component. |
| <br>Create                     | <br>Physician_Liaison_Home_Page                                 |                       | <br>Lightning Page                   | <br>This is a brand new component. |
| <br>Create                     | <br>Case_Record_Page1                                           |                       | <br>Lightning Page                   | <br>This is a brand new component. |
| <br>Create                     | <br>Contact_Record_Page_PRM                                     |                       | <br>Lightning Page                   | <br>This is a brand new component. |
| <br>Create                     | <br>Account_Record_Page_PRM                                     |                       | <br>Lightning Page                   | <br>This is a brand new component. |

