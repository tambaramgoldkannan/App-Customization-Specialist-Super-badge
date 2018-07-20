App Customization Specialist

https://trailhead.salesforce.com/en/superbadges/superbadge_lightning_platform_app_builder

![Completed Badge](https://github.com/Londoner1234/App-Customization-Specialist-Super-badge/blob/master/Finished.PNG)



What You’ll be Doing to Earn This Superbadge
Add a record type
Build fields
Create an approval process
Create reports and a dashboard
Build an app and app home page


Concepts Tested in This Superbadge
Record types
Schema
Approval process
Reports
App Builder


Duration: 4 hrs - 6 hrs Estimated
Prework and Notes
Grab a pen and paper. You may want to jot down notes as you read the requirements.

Create a new Trailhead Playground for this superbadge. Using this org for any other reason might create problems when validating challenges.

Install the unmanaged package to implement Volunteer Tracker assets for all users. If you have trouble installing a managed or unmanaged package or app from AppExchange, follow the steps in this article.

Some of the terminology used in this superbadge is descriptive and may not match the name as it appears in the UI. This is to test your knowledge of Salesforce features and to find the correct one to satisfy a business need.

Use Case
Ursa Major Solar, Inc., purveyor of high-quality solar energy equipment, is interested in encouraging volunteerism among its employees. Management cares about improving their community and understands the benefits of volunteerism to their employees’ and company’s health.

Employees encouraged to volunteer feel more positively toward their employer, and they have reduced absenteeism thanks to improved health and happiness.

While volunteering, employees learn more skills or gain experiences that let them take on new business responsibilities.

By encouraging employees to volunteer on company time, the company invests in and gives back to the community that it’s a part of.

Tracking employee volunteering provides additional benefits, including showing individual progress toward goals and providing the number of hours given overall and to specific community groups.

At Ursa Major Solar, you’ve been working with another admin to build Volunteer Tracker, an app employees can use to sign up for and track volunteering hours. Previously, you worked at a nonprofit that used Salesforce’s Volunteers for Salesforce app to manage events and volunteers (to learn more, check out the Manage Volunteers for Nonprofits trail*) and will draw on this experience building a new app for Ursa Major Solar: Volunteer Tracker.

Maria, the other admin working with you on the app, just left for a weeklong volunteering trip, and she asked you to finish the final pieces of the app on your own. You will wrap up the schema, connect some fields, create some clever logic, and build easy ways for users to sign up for and manage their volunteering. Wait, can you log these hours as volunteering?

Key Stakeholders
The Volunteerism Board contributing to this project includes interested parties from different departments. Your key stakeholders are:

Dan Wong (human resources)

Maria Jimenez (system administrator)

Standard Objects
The Volunteer Tracker app uses these standard objects:

Account—a nonprofit organization where employees can volunteer their time. Ursa Major maintains a list of eligible nonprofits around the world.

User—the employee record used for tracking event sign-ups and hours volunteered. This could be you.

Custom Objects
Giving your time as a volunteer is as simple as showing up, but tracking and organizing volunteering efforts requires a well-planned schema of custom objects interacting with standard objects. These custom objects make sure volunteer opportunities, shifts, and sign ups are recorded and hours allocated correctly:

Volunteer Activity—a specific event for the volunteer organization, for example a Fall fundraising bake sale for a local animal rescue organization.

Volunteer Jobs—the work, or tasks, to do related to the activity, for example a money handler for the bake sale.

Volunteer Shifts—the day or time slots (or slot) for the volunteer job, for example the money handler needs morning and afternoon shifts covered over 2 days.

Volunteer Shift Workers—the individual occupying one of the slots for the shift, for example Maria Jimenez signed up for the morning shift on both days. This custom object makes it possible to have multiple users as workers assigned to one volunteer shift, and multiple shifts assigned to each worker.

Entity Diagram
entity diagram

Business Requirements
Volunteer Organization Creation
The best Volunteer Tracker can’t help anyone without volunteer organizations, but Ursa Major Solar wants to ensure organizations meet certain criteria before activities can be created for them. The Volunteerism Board will research each organization and confirm it is a valid not-for-profit benefiting the community before the first volunteer activity can be created.

To get started, install the unmanaged package. Then create the new Volunteer Organization Status field determining whether activity creation is allowed for the org, the unique page for volunteer organizations with the subset of account fields needed, the record type bringing it all together, and a compact layout.

New Field
Field label	Volunteer Organization Status
Options	
Pending Approval
Accepting Activities
Retired
Use Pending Approval as the default.
Security	
System Administrator: Visible
All others: Visible and Read-only
Also, provide edit access to this field on an individual-by-individual basis without modifying profiles. Call this solution "Volunteerism Board".
New Layouts
Page layout name	Volunteer Organization Account Page Layout
Account fields displayed	
Account Name
Account Number
Account Owner
Description
Phone
Website
Shipping Address
Volunteer Organization Status
Parent Account
Compact layout name	Volunteer Organization Account compact layout
Account fields displayed	
Account Name
Phone
Volunteer Organization Status
Compact layout assignment	Volunteer Organization Account record type
New Record Type
Label	Volunteer Organization Account
Description	Account page for creating volunteer organizations
Accessibility	Enabled for all Profiles
Settings	Use the Volunteer Organization Account Page Layout
Expand Your App
With volunteer organizations now available, it is time to build out the rest of the app schema. Maria helped you sketch out how the objects are related and the fields that will let them interact. All fields should be available to all profiles and added to respective page layouts unless indicated otherwise. Let’s get building!

Relationships
The correct relationships between objects ensure volunteer data can be used in reporting, records are deleted correctly, and field information can be in parent or child fields. Use the entity diagram and this chart to establish relationships between the Volunteer Tracker objects.

Field Label	Field Purpose
Volunteer Shift	Connects Volunteer Shift Workers to Volunteer Shifts with cascading delete and the option of roll-up summary fields.
Volunteer	Connects Volunteer Shift Workers to the user.
Volunteer Job	Connects Volunteer Shifts to Volunteer Jobs with cascading delete and the option of roll-up summary fields.
Volunteer Activity	Connects Volunteer Jobs to Volunteer Activity. A value should be required to save.
Volunteer Organization	Connects Volunteer Activity to Account with the option of roll-up summary fields. Only accounts with the record type we created of status Accepting Activities should be eligible to select.
Shift Tracking Fields
Organizing volunteering without the ability to sign up for, manage, and report on shifts is like maintaining a community garden without a good pair of gloves. These fields will help track shift status and volunteer counts.

Field Label	Field Purpose
Status	The Volunteer Shift Worker record tracks whether or not the volunteer has confirmed or showed for their shift. Default of this required field is Unconfirmed. Status options are:
Unconfirmed
Pending Approval
Confirmed
Completed
No-Show
Canceled
Desired # of Volunteers	The Volunteer Shift object captures how many volunteers are required from the user. This required field allows whole numbers up to three digits.
Shifts Taken	Volunteer Shift displays the cumulative number of Confirmed or Completed Volunteer Shift Workers.
# of Volunteers Still Needed	Volunteer Shifts calculates and displays the difference between the number of required volunteers and the shifts taken, or zero, whichever is greater.
Field Label	Field Purpose
Number of Shifts	Volunteer Jobs displays the cumulative number of its shifts.
Cumulative Volunteers Needed	Volunteer Jobs displays the cumulative number of volunteers still needed for all its shifts.
Hours Tracking Fields
Wait, when was my shift again? Detailing the start and end times of shifts is key for volunteers to know when to show up for their shift. The Volunteer Tracker app will use this information to show volunteers their total hours and track top volunteers and organizations.

Field Label	Field Purpose
Shift Start Time	The Volunteer Shift record stores the date and time a shift should begin. This field is required.
Shift End Time	The Volunteer Shift record stores the date and time a shift should complete. This field is required. Build a rule called "Start before End" ensuring that Shift End Time comes after Shift Start Time with the error message, "No time travel allowed during volunteering! Shift Start Time must be before Shift End Time."
Shift Hours	Volunteer Shift calculates the number of hours a shift lasts from the start and end times.
Total Vol Hours for Shift	Volunteer Shift calculates the total number of all hours allocated to this shift from all the assigned volunteers. Calculate it using the Shift Hours and Shifts Taken fields.
Field Label	Field Purpose
Shift Hours	Volunteer Shift Workers displays this value from the associated Shift record.
Shift Start Time	Volunteer Shift Workers displays this value from the associated Shift record.
Shift End Time	Volunteer Shift Workers displays this value from the associated Shift record.
Attributed Volunteer Hours	Volunteer Jobs displays the cumulative number of volunteer hours for its shifts.
Other Fields
With the relationships built, shifts tracked, and hours calculated, what else is there? These fields make using the Volunteer Tracker app more useful, provide better reporting, and more.

Field Label	Field Purpose
Volunteer Skills	The User and Volunteer Job should have a picklist where multiple skills can be chosen. Only create the values for this field once, calling it Volunteer Skills Values. The selectable skills are:
Accounting
Computers
Tutoring
Fundraising
General manual labor
Create a picklist on the User and Volunteer Jobs objects called Volunteer Skills using this value set.
IsShiftVolunteer	This checkbox, on the Volunteer Shift Worker record, is automatically checked if the user looking at a record is also the Volunteer, and is unchecked if it is not. This field will be vital to reporting on a volunteer’s specific information.
Volunteer Organization	Volunteer Job, Volunteer Shift, and Volunteer Shift Worker display the associated Organization name.
Volunteer Activity	Volunteer Shift and Volunteer Shift Worker display the associated Activity name.
Volunteer Job	Volunteer Shift Worker displays the associated Job name.
Job Description	Volunteer Job allows users to enter a summary of the job with the option for hyperlinked text for e-volunteering websites.
Automate Shift Confirmation Approval
The biggest worry for volunteer coordinators, other than running out of coffee, is that volunteers fail to show for their shift. Your nonprofit experience tells you that a major cause of volunteer absenteeism is a well-meaning friend or coworker signing someone up without their knowledge. Signing up a friend is also a big source of referrals, so allowing only self sign up won’t work. Instead you need to build in logic for a volunteer to confirm they’re going to show up if someone else signs them up.

For the confirmation, Maria suggested using an approval process with these notes:

Name the process Confirm Volunteer Shift.

While awaiting confirmation from the Volunteer, set the status to Pending Approval.

Update the status to Confirmed if approved by the volunteer, otherwise change to Canceled.

While the approval process will manage getting the confirmation, another automation tool will be needed to kick off the process. Call this tool Launch Shift Approver. Use this same tool to update the Volunteer Shift Worker record status to Confirmed if someone signed themselves up.

Create Another User for Testing
Testing the volunteer shift approval process without another user is like trying to clear a downed tree from a hiking trail by yourself—it just doesn’t work. Dan offered to help your testing. Create a new user for Dan with these settings:

Name	Dan Wong
Email	Your email address
Role	Western Sales Team
Username and Nickname	Follow this formula: DWong @ your initials + today’s date in a 6-digit format + .com For example: DWong@tm012618.com
User License	Salesforce
Profile	Custom: Sales Profile
Quick Self Sign Up
Maria asked for a quick way for users to sign themselves up for a Shift directly from a Volunteer Shift record. Your solution was an action with the label Sign Me Up. To keep it simple there should be no fields on the pop-up. Instead the action automatically sets the Volunteer to the user clicking the button, changes the status to Confirmed, and assigns the currently viewed Shift as the new record's Volunteer Shift. Once the action is done show the friendly message "Congratulations, you are signed up!".

Report on App Data
The ability to accurately report on top volunteers, organizations, and other metrics is what separates the Volunteer Tracker from—shudder—the sign-up sheet on a clipboard in the Ursa Major break room the Volunteerism Board has been using. To accomplish this, Maria helped you map out two custom report types, five reports, and a dashboard that will come into play when surfacing the app. A couple of notes before getting started:

Create the folders Volunteer Reports and Volunteer Dashboards and store reports and the dashboard in their correct respective folder.

Continuous testing and reevaluation is key for a successful app builder to create a valuable product that matches project requirements. As such, you’ve likely created a number of different volunteer activities, volunteer jobs, and other records for testing along the way. If not, do so now—or these reports will be very sparse.

Users with Volunteer Shift Worker Records
This report type, Users with Volunteer Shift Worker Records, enables reports on Users if they have at least one associated Volunteer Shift Worker.

Accounts with Volunteer Activities with Volunteer Jobs
For this report type, Accounts with Vol Activities with Vol Jobs, include Accounts with at least one Volunteer Activity that have at least one Volunteer Job associated.

My Top Volunteer Organizations
Climbing a mountain feels less like work and more like an accomplishment when you look back and see how far you’ve come. In the same way, the My Top Volunteer Organizations report shows each user which organizations they’ve volunteered with, the time volunteered, and the total volunteer hours. Using the custom report type with user data, create a Summary report grouped by Volunteer Organization showing each organization’s cumulative hours and no other columns. Sort high to low by hours. Details aren’t necessary. The report should include only shifts where the volunteer confirmed or showed up, and it should display only records where the user viewing it is the volunteer.

My Shifts Pending Approval
Did your well-meaning teammate sign you up for a shift again without asking? The My Shifts Pending Approval report will show a user which of their shifts still need to be confirmed or canceled. Using the custom report type with user data, create a Tabular report showing the Volunteer Shift Worker ID, Shift Start Time, Volunteer Activity, Volunteer Job, and Volunteer Organization. Only pending shifts for this volunteer should be displayed.

My Upcoming Shifts
Even the best volunteers need a reminder now and then. The My Upcoming Shifts report shows a user which of their confirmed shifts are starting in the next 30 days. Using the custom report type with user data, create a Tabular report showing the Volunteer Shift Worker ID, Shift Start Time, Volunteer Activity, Volunteer Job, and Volunteer Organization. Only confirmed shifts for this volunteer should be displayed.

Top Volunteer Organizations
A friendly competition has developed in the office to see which volunteer organizations can accrue the most hours. The Top Volunteer Organizations report and report chart fan the flames of this competition. Using the custom report type with account data, the summary report shows a list of Volunteer Organization Accounts with each org’s attributed volunteer hours, ranked from most to least hours. Details aren’t necessary. The report chart is a horizontal bar chart called Top Volunteer Organizations showing the attributed hours as the x-axis.

Top Volunteers
Top volunteers are rewarded with praise, affection, recognition at major company events, and high-fives at Ursa Major. The Top Volunteers report and report chart help these volunteers prepare for fame. Using the custom report type with user data, the summary report groups by the volunteer’s name and summarizes each volunteer’s hours. Be sure the report includes only completed hours, hides details, and sorts volunteers from most hours to least. The report chart is a horizontal bar chart called Top Volunteers showing the shift hours as the x-axis.

My Volunteer Information Dashboard
The My Volunteer Information dashboard brings reports together on one dashboard to provide each volunteer visibility into their commitments, progress, and pending shifts.

Title	Footer	Source Report	Component Details
My Top Volunteer Organizations	Total hours displayed inside chart	My Top Volunteer Organizations	
Donut Chart
Sort Rows By: Value Ascending
Max Values Displayed: 5
Component size: 3 cells wide and 6 cells high
Positioned in upper left
My Volunteer Shifts Needing Approval	Click the "Shift-XXXX" to confirm or cancel the shift.	My Shifts Pending Approval	
Lightning Table
Columns:
- Volunteer Shift Worker ID
- Shift Start Time
- Volunteer Job
- Volunteer Activity
Sort Column: Shift Start Time
Sort Ascending
Max Groups Displayed: 5
Component size: 6 cells wide and 3 cells high
Positioned in upper right
My Upcoming Confirmed Shifts		My Upcoming Shifts	
Lightning Table
Columns:
- Volunteer Shift Worker ID
- Shift Start Time
- Volunteer Job
- Volunteer Activity
Sort Column: Shift Start Time
Sort Ascending
Max Groups Displayed: 5
Component size: 6 cells wide and 3 cells high
Positioned in bottom right
Surface the App
Dan and the rest of the Volunteerism Board think the app functionality is awesome, and the reports beautiful, but that there would be more time for volunteering if the app was surfaced conveniently. Your task is to bring all the pieces together in one Lightning app with a Lightning app home page showing the volunteer data.

Lightning App Details
App Name	Volunteer Tracker
Image	Assign any image of your choosing that encourages volunteerism.
Selected Items	
Accounts
Volunteer Activities
Volunteer Jobs
Volunteer Shifts
Volunteer Shift Workers
Selected Profiles	
Custom: Sales Profile
System Administrator
Standard User
Lightning App Page Details
Label	Volunteering Data
Layout	Header and Three Columns
Top component	My Volunteer Information Dashboard
Bottom left component	Top Volunteer Organizations report chart
Bottom middle component	Top Volunteers report chart
Bottom right component	Five recent items from Volunteer Activity and Volunteer Jobs with label "Recently Viewed Activities and Jobs"
Icon	Any icon you feel is appropriate
Lightning App Placement	On the Volunteer Tracker at the top of the list
Mobile App Placement	Between Events and Approvals
Resources
If you are interested in a volunteer tracking app for your nonprofit or for-profit company, consider installing the open source Volunteers for Salesforce app from the app store. It allows additional reporting, sign ups for non-Salesforce users through a website, a job shift calendar, and more.
Ready to tackle this superbadge? ver. 2018-03-08 12:00 pm
