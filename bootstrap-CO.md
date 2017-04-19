# Bootstrap a new CO

Step 1: Create the new CO
Step 2: Create a new extended type to use as the type for a generic CO identifier
Step 3: Create a new identifier assignment to auto-generate the generic CO identifier values
Step 4: Create a basic self-signup with approval enrollment
Step 5: Create an LDAP directory branch for the new CO
Step 6: Configure an LDAP Provisioner
Step 7: Test enrollment
Step 8: Promote your test enrollment to be a CO admin
Step 9: Enroll the first CO admin
Step 10: Expunge your own CO Person record

## Step 1: Create the new CO
1. Determine a short name or acronym for the organization to use as the name of the CO. For example, "UIDI" for Uganda's Infectious Diseases Institute..
2. Log into the registry as a platform administrator.
3. Click the "Platform" menu and choose "COs".
4. Click "Add CO".
5. In the "Name" field enter the short name or acronym for the organization, preferably WITHOUT spaces.
6. In the "Description" field enter the full name and/or description for the organization.
7. Leave "Status" as "Active".
8. Click "Add".
9. Click the "Collaborations" menu and choose the CO you just created to make it the active CO.

## Step 2: Create a new extended type to use as the type for a generic CO identifier
1. Click the "Configuration" menu and choose "Extended Types".
2. Make sure that "Identifier (CO Person)" is the chosen selection for "For Attribute" drop-down list (it is the default).
3. Click "Add Extended Type".
4. For the "Name" field take the name of the CO, lowercase it, and append "id" (no space). For example if UIDI is the name of the CO then enter "UIDIid".
5. For "Display Name" enter the name of the CO followed by "ID" (include a space). For example if UIDI is the name of the CO then enter "UIDI ID".
6. Leave Status as "Active".
7. Click "Add".

## Step 3: Create a new identifier assignment to auto-generate the generic CO identifier values
1. Click the "Configuration" menu and choose "Identifier Assignments".
2. Click "Add Identifier Assignment".
3. For "Description" enter the name of the CO followed by "ID" (include space). For example, if UIDI is the name of the CO then enter "UIDI ID".
4. For "Type" choose the type you created in the previous step (eg. UIDI ID).
5. Leave "Email Type" with no selection (the default).
6. Leave "Login" unchecked (the default).
7. Leave "Algorithm" as "Sequential" (the default).
8. For "Format" enter the name of the CO followed by "(#)". If the name of the CO is more than 4 characters consider an appropriate abbreviation, for example "ScienceForum" might be abbreviated to "SF" so that you enter "SF(#)". Notes: (1) The "4 character abbreviation" is just a suggestion to try to keep the identifiers short. (2) It is important to make the abbreviation unique so that there are not LDAP collisions.
9. You can leave the Pattern drop-down list as "Select a Common Pattern".
10. Leave "Permitted Characters" as "AlphaNumberic Only" (the default).
11. For "Minimum" enter "1000000" (1 followed by 6 zeros).
12. Click "Add".

## Step 4: Create a basic self-signup with approval enrollment
1. Click the "Configuration" menu and choose "Enrollment Flows".
2. Click "Add/Restore Default Templates".
3. Find the "Self Signup with Approval (Template)" flow and click "Duplicate" to create a copy of it.
4. Locate the copy you just created and click "Edit".
5. Use the following as a template (change the name of the CO in appropriate places):
* Name: UIDI Registration: Self Signup With Approval
* Status: Active
* Petitioner Enrollment Authorization: Authenticated User
* Identity Matching: None
* Require Approval for Enrollment: checked, empty Approvers
* Email Confirmation Mode: Automatic
* Invitation Validity: 1440
* Verification Email Message Template: blank
* Subject for Verification Email: Please verify your UIDI Registration
* Verification Email Body:
> Thank you for registering with the UIDI Registry.
>
> Before your registration can be approved you need to visit the link below so that we can verify that you received this email at an email address you control.
>
> After you click the link and verify your registration an administrator from the UIDI VO will review you registration for accuracy as soon as possible and then approve it. You will receive another email after the registration is completed.
>
> (@INVITE_URL)
>
> Thank you,
>
> UIDI administrator team


* Require Enrollee Authentication: checked
* Duplicate Enrollment Mode: Flag as Duplicate
* From Address for Notifications: leave blank
* Notifications Group: leave blank
* Notify on Approved Status: check
* Approval Email Message Template: leave blank
* Subject for Approval Email: (@CO_NAME) Registration has been approved
* Approval Email Body:

> Your registration with the (@CO_NAME) VO is now complete.
>
> Thank you for registering.
>
> (@CO_NAME) administrator team
>

* Notify on Finalization: leave unchecked
> Introduction:
> Please click below to begin the registration process for the (@CO_NAME) VO Registry. You will be asked to submit a form with your home institution, name, and email address. After you verify your email address and your application is approved you will receive another email when your registration is complete.

* Conclusion:
> After submitting the form you will receive an email asking you to click and verify your registration. You will receive another email after your registration has been approved by (@CO_NAME) VO staff.

* Terms and Conditions Mode: Ignore
* Submission Redirect URL: leave blank
* Confirmation Redirect URL: leave blank
* Ignore Authoritative Values: leave unchecked
* Theme: leave blank
6. Click "Save".
7. Click "Edit Enrollment Attributes".
8. Click "Edit" next to the "Organization" attribute:
* Label: Identity Provider
* Description: The identity provider you used to log in to this site.
* Attribute: Organization (Organizational Identity)
* Required: Require
* Ignore Authoritative Values: leave unchecked
* Order: ignore for now
* Default value: leave blank
* Modifiable: unchecked
* Hidden: unchecked
* Click "Save" to save your changes.
9. Click "Edit" next to the "Name" attribute:
* Label: Name from your Identity Provider
* Description:
* Leave the rest of the fields as they are and click "Save"
10. Click "Edit" next to the "Email" attribute:
* Label: Email address from your Identity Provider
* Description:
* Attribute: Email (Official, Organizational Identity)
* Copy this attribute to the CO Person record: checked
* Required: Required
* Ignore Authoritative Values: unchecked
* Order: ignore
* Click "Save" to save your changes.
11. Click "Edit" next to the "Affiliation" attribute:
* Check "Ignore Authoritative Values"
* Default Value: Member
* Modifiable: unchecked
* Hidden: checked
* Click "Save" to save your changes.
12. Click "Add Enrollment Attribute".
* Label: Preferred Name
* Description: Your desired display name (optional)
* Attribute: Name (Preferred, CO Person)
* Required: Optional
* Ignore Authoritative Values: leave unchecked
* Order: ignore
* Click "Add" to add the enrollment attribute.
13. Click "Add Enrollment Attribute".
* Label: Preferred Email
* Description: Your preferred email address (optional)
* Attribute: Email (Preferred, CO Person)
* Required: Optional
* Ignore Authoritative Values: leave unchecked
* Order: ignore
* Click "Add" to add the enrollment attribute.
14. Click "Reorder Attributes" and use the GUI to order the attributes top-to-bottom in the order
* Identity Provider
* Name
* Preferred Name
* Email
* Preferred Email
* Affiliation
15. Click "Done" to save the ordering.


## Step 5: Create an LDAP directory branch for the new CO
1. SSH into the host for the LDAP directory (e.g., comanage1).
2. Create a text file following this template, replacing "UIDI" with the 4 character abbreviation you created in step 3.8:

`dn: o=UIDI,dc=fiamvro,dc=org
objectclass: dcObject
objectclass: organization
dc: fiamvro
o: UIDI

dn: ou=people,o=UIDI,dc=fiamvro,dc=org
objectclass: organizationalUnit
ou: people

dn: ou=groups,o=UIDI,dc=fiamvro,dc=org
objectclass: organizationalUnit
ou: groups

dn: ou=system,o=UIDI,dc=fiamvro,dc=org
objectclass: organizationalUnit
ou: system

dn: uid=registry_user,ou=system,o=UIDI,dc=fiamvro,dc=org
objectclass: account
objectclass: simpleSecurityObject
uid: registry_user
description: FIAMVRO Registry user for UIDI
userPassword: <see next step>`


3. Create a 20 character password using lower case letters, upper case letters, and digits. Note the password.
4. Switch to root for the next commands.
5. Execute the command `/root/generate_password_hash.sh`. When prompted enter the 20 digit password (twice).
6. Copy the output and use it for the value of "userPassword" in the template above. It should look something like this (it is long and does not line break nicely in this document):

`{CRYPT}$6$rounds=5000$MBwBXJ8BTA5I4pPo$bXTzMbxwT3hNrptJY8FA0DRyk3I3muVLluJ2kRd2frfZd15VkYnQQurbguO20/lC7ap9CbkbaaBKIurcO8Ne4.`


7. Be sure none of the lines in the file have whitespace at the end.
8. Be sure there is no extra line at the end of the file.
9. Obtain from the Shared-FIAMVRO 2 LastPass folder the password for the LDAP admin account with DN cn=admin,dc=fiamvro,dc=org.
10. Execute the command

`ldapadd -x -W -H ldapi:/// -D "cn=admin,dc=fiamvro,dc=org" -f <LDIF FILE>`

where <LDIF FILE> is the file you just created from the template above. When prompted enter the password for the LDAP admin user.
11. Edit the file `/root/modify_olcaccess.ldif`. You need to ADD another line after the existing lines but BEFORE the last line, use the appropriate number, and increment the number of the last line. BE SURE TO CHANGE THE NAME OF THE CO IN TWO PLACES IN THE NEW LINE.
12. Execute the command

`ldapmodify -Y EXTERNAL -H ldapi:/// -f modify_olcaccess.ldif`


13. Record the password for the new registry_user DN that you just created in the shared FIAMVRO2 LastPass folder following the existing examples.


## Step 6: Configure an LDAP Provisioner
1. Click the "Configuration" menu and choose "Provisioning Targets".
2. Click "Add Provisioning Target".
* Description: Primary LDAP
* Plugin: LdapProvisioner
* Provisioning Group: leave blank
* Status: Automatic Mode
* Order: ignore
* Click "Add" to create the new provisioner.
3. Edit the provisioner details:
* Server URL: ldap://127.0.0.1
* Bind DN: the DN of the registry_user you just created following the template
* uid=registry_user,ou=system,o=UIDI,dc=fiamvro,dc=org
* Password: the password for the registry_user DN (from step 5.3)
* People DN Identifier Type: the identifier you created earlier, eg. UIDI Identifier
* People DN Attribute Name: employeeNumber
* People Base DN: ou=people,o=UIDI,dc=fiamvro,dc=org
* Group Base DN: ou=groups,o=UIDI,dc=fiamvro,dc=org
* Attribute Scope: leave blank
* Unconfigured Attribute Mode: Remove
* Click "Save" to save the provisioner.

## Step 7: Test enrollment
1. Click on the "People" menu and choose "Enroll".
2. Right-click on the "Begin" button next to the existing enrollment flow to record the URL.
3. In a private-browsing window visit the URL and complete the enrollment process. Be sure to only evaluate the link in the email in your private browsing window, not the window you are using as the platform administrator.
4. After "clicking the link" in the email as the platform administrator click on the "People" menu and choose "CO Petitions".
5. Click "View" to view the petition.
6. Click "Approve" to approve the petition.
7. Click the "People" menu and choose "My Population".
8. Click "Edit" next to the CO Person record.
9. Verify the details of the record in particular that the auto-generated identifier (eg. UIDI ID) was created for the record.
10. Use the password for the registry_user DN to verify that a record was created in LDAP by the provisioner, e.g.,

`ldapsearch -LLL -x -W  -H ldapi:/// -D "uid=registry_user,ou=system,o=UIDI,dc=fiamvro,dc=org"  -b "ou=people,o=UIDI,dc=fiamvro,dc=org"`

`dn: employeeNumber=UIDI100000,ou=people,o=UIDI,dc=fiamvro,dc=org
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: eduMember
sn: Koranda
cn: Scott Koranda
givenName: Scott
mail: skoranda@uwm.edu
employeeNumber: UIDI100000
uid: skoranda@uwm.edu
isMemberOf: members`

## Step 8: Promote your test enrollment to be a CO admin
1. Click on "Groups" and choose "All Groups".
2. Click on the "admin" group.
3. Click "Manage Group Memberships".
4. Check "Member" to add your CO Person record to the admin group and make yourself a CO admin. This is convenient because you will receive a notification when the first "real" CO admin has enrolled and is ready to be promoted to CO admin (see below).

## Step 9: Enroll the first CO admin
1. Click on the "People" menu and choose "Enroll".
2. Right-click on the "Begin" button next to the existing enrollment flow to record the URL.
3. Send an email to the first CO admin and ask him/her to click on the link and complete the flow.
4. Check for a submitted petition. Inspect it as above and approve it and verify a record is provisioned into LDAP.
5. Click on "Groups" and choose "All Groups".
6. Click on the "admin" group.
7. Click "Manage Group Memberships".
8. Check "Member" to add the CO Person to the admin group and make the CO Person a CO admin.
9. Send an email to the CO admin to let him/her know that he/she is now a CO admin and able to continue with the configuration of the CO. Point him/her to the documentation, right now only https://spaces.internet2.edu/display/COmanage/COmanage+Technical+Manual

## Step 10: Expunge your own CO Person record
1. Click the "People" menu and choose "My Population".
2. Click "Edit" next to the your CO Person record.
3. Click "Expunge".
4. Check the box to confirm and then click "Expunge".
