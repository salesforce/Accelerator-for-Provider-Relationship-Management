# README.md


Updated Install Instructions
3/16/2023



# Accelerator for PRM - Unmanaged Package Installation Instructions


Last Updated: March 2023


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

[Image: Screenshot 2023-03-15 at 10.59.48 AM.png]**Configure Recommendation Record -** This Recommendation will show as a Next Best Action to your liaisons as they review contact records in Salesforce. If the custom field “Enrolled in Provider Portal?” on the Contact Record is Unchecked, then this recommendation will show.


1. Download the recommendation_1.csv file in the GitHub repository above
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

[Image: Screenshot 2023-03-15 at 11.48.54 AM.png]

1. On the Flow path, Click to add a Schedule Trigger:
    1. Set the Schedule Path to be “1 Day Before Event: Date”
    2. Time Source: Event: Due Date Only
    3. Offset Number: 1
    4. Offset Options: Day Before

[Image: Screenshot 2023-03-16 at 10.10.29 AM.png]

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




|
**Component Type**	|
**Component Name**	|
|---	|---	|
|
Lightning App	|
Physician Relationship Management	|
|
Default Home Page - PRM App	|
Physician_Liaison_Home_Page	|
|
Case Record Type	|
Account Request	|
|
Case Page Layout	|
Account Request	|
|
Case Path	|
Account Request Path	|
|
Case Lightning Page	|
Case_Record_Page1	|
|
Task Record Type	|
Simple Task	|
|
Contact Page Layout	|
Physician Layout	|
|
Contact Lightning Page	|
Contact Record Page PRM	|
|
Contact Compact Layout	|
Physician Liaison Layout	|
|
Lead Record Type	|
Provider	|
|
Lead Page Layout	|
Provider	|
|
Lead Lightning Page	|
Lead_Record_Page_PRM	|
|
Lead Compact Layout	|
Physician Liaison Layout	|
|
Account Page Layout	|
Account Layout - PRM	|
|
Account Lightning Page	|
Account Record Page PRM	|
|
Account Compact Layout	|
Physician Liaison Layout	|



## Unmanaged Package Component Inventory




|
Resources:	|
	|
	|
	|
	|
|---	|---	|---	|---	|---	|
|
**Action**	|
**Component Name**	|
**Parent Object**	|
**Component Type**	|
**Installation Notes**	|
|
Create	|
NewEventPRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Account Layout - PRM	|
Account	|
Page Layout	|
This is a brand new component.	|
|
Create	|
NewCasePRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
SendEmailPRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
My Accounts Without Recent Activity	|
	|
Report	|
This is a brand new component.	|
|
Create	|
Task.Defer_Change_Date	|
Task	|
Action	|
This is a brand new component.	|
|
Create	|
Screen_Shot_20220215_at_45040_PM1	|
	|
Asset File	|
This is a brand new component.	|
|
Create	|
Account Request	|
Case	|
Page Layout	|
This is a brand new component.	|
|
Create	|
NewNotePRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Physician Liaison Performance Dashboard	|
	|
Dashboard	|
This is a brand new component.	|
|
Create	|
Account_Request_Path	|
	|
Path Assistant	|
This is a brand new component.	|
|
Create	|
Provider	|
Lead	|
Business Process	|
This is a brand new component.	|
|
Create	|
My Check Ins	|
	|
Report	|
This is a brand new component.	|
|
Create	|
Simple Task	|
Task	|
Page Layout	|
This is a brand new component.	|
|
Create	|
SampleHealthcarePractitionerFacilityContactConfigurationPRM	|
	|
UI Object Relation Configuration	|
This is a brand new component.	|
|
Create	|
Provider	|
Lead	|
Record Type	|
This is a brand new component.	|
|
Create	|
Provider	|
Lead	|
Page Layout	|
This is a brand new component.	|
|
Create	|
Confirm Meeting	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Account Request	|
Case	|
Business Process	|
This is a brand new component.	|
|
Create	|
My Completed Activities	|
	|
Report	|
This is a brand new component.	|
|
Create	|
Liaison Reports	|
	|
Report Folder	|
This is a brand new component.	|
|
Create	|
Physician Liaison Layout	|
Account	|
Compact Layout	|
This is a brand new component.	|
|
Create	|
Case.SendEmailCase	|
Case	|
Action	|
This is a brand new component.	|
|
Create	|
Enroll in Provider Portal	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Physician Liaison Layout	|
Contact	|
Compact Layout	|
This is a brand new component.	|
|
Create	|
LogACallPRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Simple Task	|
Task	|
Record Type	|
This is a brand new component.	|
|
Create	|
My Avg Check-In Distance from Account (f	|
	|
Report	|
This is a brand new component.	|
|
Create	|
NewTaskPRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Physician Layout PRM	|
Contact	|
Page Layout	|
This is a brand new component.	|
|
Create	|
Salesforce Maps Check Out	|
Task	|
Field Set	|
This is a brand new component.	|
|
Create	|
Referral Trend Report	|
	|
Report	|
This is a brand new component.	|
|
Create	|
NewOpportunityPRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Task.UpdatePriority_PRM	|
Task	|
Action	|
This is a brand new component.	|
|
Create	|
General	|
Task	|
Record Type	|
This is a brand new component.	|
|
Create	|
My New Leads	|
Lead	|
List View	|
This is a brand new component.	|
|
Create	|
NewContactPRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Account Request	|
Case	|
Record Type	|
This is a brand new component.	|
|
Create	|
My Meeting Quality	|
	|
Report	|
This is a brand new component.	|
|
Create	|
My Time Spent On Site	|
	|
Report	|
This is a brand new component.	|
|
Create	|
SampleHealthcarePractitionerFacilityAccountConfigurationPRM	|
	|
UI Object Relation Configuration	|
This is a brand new component.	|
|
Create	|
Physician Liaison Layout	|
Lead	|
Compact Layout	|
This is a brand new component.	|
|
Create	|
Liaison Dashboards	|
	|
Dashboard Folder	|
This is a brand new component.	|
|
Create	|
New_Task_PRM	|
Global	|
Action	|
This is a brand new component.	|
|
Create	|
Task.UpdateStatusPRM	|
Task	|
Action	|
This is a brand new component.	|
|
	|
	|
	|
	|
	|
|
Apps:	|
	|
	|
	|
	|
|
**Action**	|
**Component Name**	|
**Parent Object**	|
**Component Type**	|
**Installation Notes**	|
|
Create	|
Physician Relationship Management	|
	|
App	|
This is a brand new component.	|
|
	|
	|
	|
	|
	|
|
Flows:	|
	|
	|
	|
	|
|
**Action**	|
**Component Name**	|
**Parent Object**	|
**Component Type**	|
**Installation Notes**	|
|
Create	|
Reminder to Enroll in Provider Portal	|
	|
Flow Version	|
This is a brand new component.	|
|
	|
	|
	|
	|
	|
|
Fields:	|
	|
	|
	|
	|
|
**Action**	|
**Component Name**	|
**Parent Object**	|
**Component Type**	|
**Installation Notes**	|
|
Create	|
Check Out Distance From Record (mi)	|
Activity	|
Custom Field	|
This is a brand new component.	|
|
Create	|
Check Out Date/Time	|
Activity	|
Custom Field	|
This is a brand new component.	|
|
Create	|
Meeting Quality	|
Activity	|
Custom Field	|
This is a brand new component.	|
|
Create	|
Check In Date/Time	|
Activity	|
Custom Field	|
This is a brand new component.	|
|
Create	|
Enrolled in Provider Portal?	|
Contact	|
Custom Field	|
This is a brand new component.	|
|
Create	|
Time on Site Minutes	|
Activity	|
Custom Field	|
This is a brand new component.	|
|
Create	|
Days Since Last Visit	|
Account	|
Custom Field	|
This is a brand new component.	|
|
Create	|
Check Out Date	|
Activity	|
Custom Field	|
This is a brand new component.	|
|
	|
	|
	|
	|
	|
|
Recommendation Strategies:	|
	|
	|
	|
	|
|
**Action**	|
**Component Name**	|
**Parent Object**	|
**Component Type**	|
**Installation Notes**	|
|
Create	|
Referring Providers	|
	|
Recommendation Strategy	|
This is a brand new component.	|
|
	|
	|
	|
	|
	|
|
Pages:	|
	|
	|
	|
	|
|
**Action**	|
**Component Name**	|
**Parent Object**	|
**Component Type**	|
**Installation Notes**	|
|
Create	|
Physician_Relationship_Management_UtilityBar	|
	|
Lightning Page	|
This is a brand new component.	|
|
Create	|
Lead_Record_Page_PRM	|
	|
Lightning Page	|
This is a brand new component.	|
|
Create	|
Physician_Liaison_Home_Page	|
	|
Lightning Page	|
This is a brand new component.	|
|
Create	|
Case_Record_Page1	|
	|
Lightning Page	|
This is a brand new component.	|
|
Create	|
Contact_Record_Page_PRM	|
	|
Lightning Page	|
This is a brand new component.	|
|
Create	|
Account_Record_Page_PRM	|
	|
Lightning Page	|
This is a brand new component.	|

