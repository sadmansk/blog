+++
tags = ["self-hosting", "privacy", "tutorial"]
categories = ["self-hosting"]
slug = ""
date = "2017-04-29T21:59:58-04:00"
title = "Syncing private data with Nextcloud Part 1: Android"
comments = false
draft = true
showcomments = true
showpagemeta = true

+++

After putting it off for a very long time, I finally managed to set aside sometime
to write up this piece on how to make the most out of a Nextcloud deployment (note
that similar steps also apply with ownCloud instances). This guide assumes that
you already have access to a Nextcloud instance, whether you deployed it yourself
or using someone else's, throughout the guide, I'll note the base URL as `https://host.domain.com`,
and the user name and password being `USERNAME` and `PASSWORD`. Make sure to replace
these with your own credentials and URL. Anyways, let's get started.

So first of all, let me tell you what things you can get out of such an instance.
By default, Nextcloud comes with support for file syncing/sharing, even the
[Nextcloud app](https://f-droid.org/packages/com.nextcloud.client/) works for that
out of the box. However, where this application really comes to fruition is when
we take advantage of other things, such as Contacts, Calendar, Tasks (to-do lists)
syncing. At least for me, with me being so in favor of moving away from third-party
cloud services, it has completely changed the way I manage my data among my devices.
I'll also briefly cover another usage, which isn't very common, RSS feed reader.

Nextcloud uses open source protocols, CalDAV and CardDAV for syncing calendar, tasks,
and contacts. At first, I'll cover how to sync these on an Android phone, and then
move on to syncing to Desktop (skipping instructions for iphone since I don't have
access to one for now).

## Android
For file syncing, as mentioned before, you can just grab the
[Nextcloud app](https://f-droid.org/packages/com.nextcloud.client/) for free. You
can also set it up so that new photos and videos that you take are uploaded to a
specific folder in your Nextcloud account. You can tweak related settings as you
want in the app, so make sure to check that out. However, to extend the syncing
capabilities to your calendar, todo list and contacts, you need to download a
separate app that provides a bridge between the cloud and applications on your phone.

In my case, I use [DAVDroid](https://f-droid.org/packages/at.bitfire.davdroid/),
and had a really good experience so far with it, so the instructions that follow
will be directed towards the usage of DAVDroid. Although marketed as a paid app
on the Google Play Store, you can grab the app for free from Fdroid. I do suggest
buying the app or making the donation to the developers though if you like the application.

### Calendar and Tasks
In order to take advantage of the to-do list syncing, you need another app from
Fdroid, called [OpenTasks](https://f-droid.org/packages/org.dmfs.tasks/). It supports
adding of DAVDroid as a source for task syncing. Most calendar apps should work,
so I won't focus on any specific one (e.g. I'm using the default calendar app on my phone).

Once those apps are downloaded, open up the Nextcloud app, under settings, there
is an option **Sync calendar & contacts**. Just click on that, and that should take
you to "Add account" page of DAVDroid. *Maybe add screenshots here*

### Contacts
For contacts, you should already have get the option to save to your DAVDroid account
when creating new contacts. You probably would want to save all your contacts to
Nextcloud. If you do, the method varies among different Contacts apps, but the general
steps are the same. Copy the contacts list from all other sources to your DAVDroid
account, and that's it! If you want to not have your contacts list not saved in
other places (possible duplication), you may delete the duplicates, but **be super careful!**

## What's next
You should now be totally good to go. If any of the above things didn't quite work,
please throw me a shout so I can fix the guide up as well as help you troubleshoot
in the process. In a later post, I'll cover how to sync all of this on a desktop.
