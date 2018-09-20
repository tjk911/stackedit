The collections email reminder/notification app sends email notifications to staffers when collections they are responsible for is outdated.

There are a number of moving pieces for this, we'll try to touch all of them below.

## What staffers use

The URL is a little misleading, as this app has undergone various iterations, but it lives here: [Collections scheduler](http://www.spokesman.com/apps/scheduler/)

On the left, staffer should type in their own names to select themselves.

The right column should display the days of the week and a collections input box if the page is done loading. If there's a spinning color wheel, wait a little while, it should load shortly. If it doesn't - contact Kai.

Once a user is selected (on the left), the right columns should auto update to display any previously saved data. If the user hasn't used this before, all of it should be blank.

Select the days the user works (for example, Kai would be Mon-Fri), and the collections the user is responsible for by typing in the input box below (for example, Home-Promos).

User can select multiple collections and multiple days.

Click `Save schedule` and an alert should tell the user if it was successful or not.

From now onward, the user should receive notifications **once a day** if their collections are outdated, with the exception of collections that need to be updated hourly.

**_Caveat_**: if the collection was updated, but the stories weren't set to live, *no notification emails will be sent*

## The controlling files

Two key files control things:
* master.json file living on the media server
* config file living as a widget (id=290, formatted as json)

_master.json_ contains a list of our staffers, the days they work and the collections they're responsible for (as defined by themselves through the admin mentioned previously)

_config file/widget_ controls the collections that we actually care about, and whether they're supposed to be updated **daily** or **hourly**. It also logs the last time a notification was sent, so that we do not spam our staffers with emails.

What this also means is that if the collection hasn't been predefined in the config file, even if our user selects it in the admin, they **will not** receive notifications about it.

We added more matching in order to avoid spamming users and to ensure that this is, other than the initial set up, as minimally annoying as possible. Some collections need to be hourly, some need to be daily, we need the ability to easily/quickly change and add them.

## The email logic

A couple of things have to match prior to an email being sent.

1. The collection has to be outdated (as defined either daily, or hourly)
2. There's a user that has to be notified about it
3. The last notification email sent was at least an hour ago (or a day ago, depending on the collection's definition of outdated)
4. Today's day matches with a day that the user is supposed to be working
5. User has a proper staff email in their `StaffMember` profile

If all these conditions pass - an email notification will be sent.

One of the biggest things was to limit emails to daily (unless it's an hourly collection). If we send too many emails, it becomes far too easy to ignore/mute it. 

## Common possible issues

* The chronograph job does not seem to be firing consistently
* A collection wasn't added to the config file as either an _Hourly_ or _Daily_ collection

## The check_collections chronograph job

This command lives in `core/collections/management/commands/check_collections.py`.

It grabs the two config files - `master.json` and the config data from the widget - and then starts checking all of them against our list of collections.

First, it created a list of outdated collections by looping through the config file and our collections list.

Then, it loops through our master.json to check and see if anyone is responsible for those collections. After it's built out what each user is responsible for, it sends out **one** email listing all outdated collections the person has to address.

Example below:

```
Some of the collections you are responsible for are outdated, and could do with new items.  
You can add stories to collections here: [http://www.spokesman.com/sradmin/stories/story/](http://www.spokesman.com/sradmin/stories/story/)  
These are the collections that are outdated:  
diff-makers-2017  
diff-makers-2016
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbNTM1NDcyNzAyXX0=
-->