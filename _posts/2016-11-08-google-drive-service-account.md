---
layout: post
title:  "Google Drive Service Account Setup"
date:   2016-11-08 01:00:00 -0600
---

I'm working on a project that uses the Google Drive API and rather than using my
personal gmail account to authenticate I figured it would be a good idea to use
a service account.

The main issue that I ran into setting up a service account was that I needed to
share my google drive folder with my new service account. Apparently when you
setup a new service account and download the json file, it contains a special
unique email address that you can then use to share Google Drive folders with.

- https://developers.google.com/identity/protocols/OAuth2ServiceAccount
- https://console.developers.google.com/iam-admin/serviceaccounts/project?
