+++
date = "2018-06-05"
title = "DirectoryPhish: Populate GoPhish with Active Directory Data"
tags = ["PowerShell"]
aliases = "/2018/06/directoryphish-populate-gophish-with-active-directory-data"
+++

I was recently given a project to run simulated phishing attacks against a corporation of 300-500 users with email access, but was shocked to find there was no easy way to use existing Active Directory data in GoPhish. To make things more difficult, we had some complex requirements:

* We did not want to target all users at once
* This corporation has multiple internal companies with different domains
* Some internal companies opted out of the initial campaigns
* Many users have restricted email access based on AD roles

My solution was to build a tool for the job, named DirectoryPhish. DirectoryPhish is a simple, open source * PowerShell script designed to query Active Directory with optional parameters and return a CSV file that can easily be mass imported into the GoPhish web GUI.

DirectoryPhish allows you to filter out your forest for the following:

* Presence of email address in Active Directory
* Group
    * Can use both Security and Distribution groups interchangeably – for example, “I want all my `All_Staff` users”
* TLD
    * Ideal for multiple corporate domain emails living in the same forest – for example, “I want all my `All_Staff` that have `@subcompany.com` emails only”
* Group Exclusion
    *Great for wide group lookups with specific exclusionary filters – for example, “I want all my `All_Staff` except the `IT_Dept_Group`“

This project was my first real dive into PowerShell scripting, and is available on [GitHub](https://github.com/ILiedAboutCake/DirectoryPhish) with documentation and examples. If you see a better way of completing a function or wish to add functionality, feel free to fork or submit a pull request.