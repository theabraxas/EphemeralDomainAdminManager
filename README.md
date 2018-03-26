# EphemeralDomainAdminManager
A powershell webserver application which allows for temporary DA (or other privileged group) assignment and management to reduce tendencies for IT orgs to have excessive users in permissive groups.

# What is this? 
The Problem: Most IT orgs grant excessive permissions to helpdesk, systems administrators, and others who do not need them all the time. This leads to those users often doing all of their work from extremely privileged accounts which poses extreme risk if phished, from local system compromises, and is generally considered a bad practice

This Solution: This app is a web server which does a few things which are meant to reduce or elimiate some of the problems tied to Domain Administrator accounts. In particular, this application is essentially a series of scripts which run on a webserver which do the following tasks.

1) LDAP authenticated login. Only members of a certain group are allowed to authenticate past the login screen. (We'll call this group "Potential Admins" for this example.)
2) Once authenticated, the user can select a time period to have 'elevated' privileges, perhaps '1 hour', '4 hours' and '8 hours' are the avilable options
3) Once the time is selected the user submits the request and the elevation happens (added to the DA group). A special event log is present on the system with the ability to also configure email notifications for whenever the system is used.
3) A scheduled task is also created to remove the user from the DA group after the time period has expired.

# Technologies
The webserver is built on a tool called Powershell Universal Dashboard (or PoshUD) - more can be found here: https://github.com/ironmansoftware/universal-dashboard 

PoshUD provides a web framework, in powershell, which allows for secure communications, LDAP authentication, and the ability to build applications using PowerShell exclusively - which should allow adoption by standard IT organizations to be smoother.

Inside of the PoshUD application are a series of scripts to perform the actions - scripts for adding/removing the user, scripts to create scheduled tasks, and scripts to notify/log whenever the system is used.

# But, aren't there better ways to do this?
Yes, absolutely. However, most people dont. Helpdesk and Sysadmins routinely log in daily, browse the internet, read emails, and do everything else at work using their privileged accounts, this presents many risks to the organization. This solution is not the best, the best would be having as few DA accounts as possible, restricting admins to standard accounts while maintaining admin accounts with delegated admin roles and routinely validating group memberships. This is very hard for organizations of all sizes to do consistently and confidently (how often has an account been kept in a group because no one knows if anything bad will happen if it gets removed).

So yes, this is not the best solution but I believe it is many steps above the techniques currently used in most organizations and may allow IT/Security teams to start to get a better grasp on their privileged accounts.
