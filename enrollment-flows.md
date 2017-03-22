# Invitation-Based Enrollment Flow

## 1  INTRODUCTION

This guide describes the process of starting and supervising an invitation-based enrollment flow in COmanage registry when adding participants to a COU. Other types of enrollment flows are: « Account Linking », « Additional Role » and « Self-enrollment ».

## 2  SCOPE

Intended for collaboration administrators using COmanage registry.

## 3 ABBREVIATIONS AND DEFINITIONS

* CO: Collaboration Organization - A collection of people collaborating with a common workflow for adding additional collaborators and with common policies for vetting the identities of collaborators. Office of the Chief Information Officer (OCIO) is an example of a CO.

*  COU: Collaborative Organization Unit - The COU is an optional construct which allows to define an organizational structure within a CO. The workflow for enrolling people may have details specific to a COU. Institute for College Research Development and Support (ICRDS) is an example of a COU.

* IdP: Identity Provider.


## 4  PROCEDURE

### a. Inviting participants

*	Log in to COmanage registry. Ask your NIH contact for the URL if you do not have it
*	Chose your CO from « Available Collaborations ». Ask your project manager if you do not know it
*	Go to the menu « People » and click « Enroll »
*	You will land on various options, select action « Begin » for Invitation  
*	You will land on the invitation form
*	Select the relevant COU and fill in the required information : « Given Name », « Family Name » and « Email » address to which the invitation will be sent
*	Click submit

You will see a page of recapitulatory information and at the top a green box confirming that the invitation, also known as a « petition », has been created.


The participant will receive an email with the link to complete the enrollment. Advise the user to check their spam since it is possible that the invitation email ends up there.

### b. Checking petition’s status
Once you have invited participants, you will have the possibility to check on the status of their enrollment; see whether the enrollment is pending or if it has been finalized.

To do so, click on the menu « People » and select « CO petitions ».

You will find a list of the petitions issued for all existing COUs including information like the name of the participant, also known as « enrollee », the type of the enrollment flow, the name of the COU they were invited to and the times at which the petition was created and modified.

Until the participant completes the enrollment, the « Status » will show « Pending Confirmation ». Once completed, the « Status » will change to « Finalized ».

At the top right of the page, you can find the following options: **"View All"; "View Pending"**


Click « View All » to see all petitions issued. Or, click « View Pending » to see the petitions that are not yet confirmed.  Right underneath these two options, there is a filter bar with various options from which you can choose what petition’s status to be shown or hidden on your list.

Another way to supervise invitation-based enrollment flow is to go to « People » and select « My ‘Name of Your COU’ population ». There, you can check petitions issued exclusively in that COU and edit participants’ information if needed. For participants who completed enrollment, you will see « Active » next to their name. At the right top of the page, you can sort the list of participants by clicking on the following options: **"Name"; "Status"; "Created"; "Modified"**

« Created » and « Modified » refer to the time at which the petition was issued or resent.


## 5  TROUBLESHOOTING   


Here are some of the most common errors that you might run into or that a participant might report to you as a collaboration administrator as well as some advice on how to go about them:

### The participant’s IdP does not release an identifying attribute.

*"ERROR: REMOTE_USER is empty. Please check your configuration"*


In this case, you can ask the participant to enroll with their commercial identity by entering as the « organization’s name » Google for a Gmail account, Windows live for a Hotmail account or Yahoo for a Yahoo account.


### The participant reports seeing « Petition expired ».

This occurs when a participant does not accept the invitation before two weeks from the time the petition was created, which is the period of validity for a single petition. In this case, you can go to « People », select « CO Petitions », find the participant and under « Actions » click « Resend Invite ». You can also use this option in case the participant does not receive the invitation email at all.

Once you click that option for a certain participant, you will be asked to confirm resending the invitation to the user.


Click « Resend Invite » and the participant will receive another email with a new URL to complete enrollment.


### The participant reports seeing « The identifier "xxxx" is not registered ».
 
After the user accepts the invitation and enrolls with the organization name, the petition is confirmed. The user is logged out and is asked to log in again in order for her/his identity to take effect. If the user does not attempt to log in again and returns to the site at a later moment, s/he will most likely get an error saying that their identity is not registered. In this case, you can ask the user to repeat their enrollment and inform the admin to contact the support team so they can clean up the database.
