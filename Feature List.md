---
created: ["2023-09-15 16:03"]
tags: ["#List/"]
share: true
multipleRepo:
  - owner: abdulhamid-the-ottoman
    repo: myexocortex
    branch: main
    autoclean: false
  - owner: abdulhamid-the-ottoman
    repo: namazzz
    branch: main
    autoclean: false
---
# 💠 Feature List
#### Salah Tracking Feature
- Checking The Status of Daily Prayers:
		- On Time, Late
		- Not prayed (Qadha)
	- To be added features
		- Jaamaah
		- Reasons to pray in that specific time
			- Pre-defined (shopping, work, travel and etc)
			- Custom
#### Analytics Feature
- 2D Monthly view with squares of different colors 
		- vertical dimension is for salahs ( Fajr, Dhur, Asr. ..)
		- horizontal dimension is for days of the month such as 14, 15 and so on
	- Summary
		- Summary tabs such as weekly, monthly, Yearly and All-time
		- Summary is based on prayer status showing the ratio based on the selected time frame
			- %30 on time
			- %20 late
			- %50 qadha
	 - Future 
		 - Reason and time based predictions to warn on a susceptible time.
	
#### Daily Salah Personal Reminders Feature
- Medium of notifications
		- Notifications can be SMS/WhatsApp or any third party messaging app.
		- Can be a phone call or any third party calling app.
	- Frequency of notifications
		- There are 3 notifications between adhans
			- the first notification is 30 mins after adhan 
			- the middle notification is in the middle of the first and last notification. 
			- the last notification is 45 mins before the next adhan
		- Exceptions
			- Isha prayer doesn't have the last notification, instead fajr has a before notification with customizable timer to pray tahaccud.
			- Fajr prayer's last notification is based on sun rise!
	- Type of notifications
		- The first notification is in the form of a poll asking :
			- Example for Isha:
				- Did you pray Isha?
					- 4 Sunnah
					- 4 Fard
					- 2 Sunnah
					- 3 Vitr
	- Collection of Information
		- The information present in the poll for current salah is collected on next salah meaning it is editable between two
#### User Data Mobility Feature
- The goal is to collect the required information such as location, qadhas, daily prayer information
- Create an online database so that when the user changes phones, he can easily request his/her information on the new mobile device. 