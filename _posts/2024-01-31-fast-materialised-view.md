---
layout: post
title: Fast Materialised View
date: 2024-01-31 19:37 +0000
description: Earliest 2024 Projects and an Oracle EBS Tip
categories: []
tags:
- Materialised Views
- Oracle EBS
- R12
status: publish
type: post
published: true
meta:
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _wpas_skip_facebook: '1'
  _wpas_skip_google_plus: '1'
  _wpas_skip_linkedin: '1'
  _wpas_skip_tumblr: '1'
  _wpas_skip_path: '1'
  publicize_twitter_user: stephenemo
  publicize_twitter_url: http://t.co/HScXosy7px
  _wpas_done_5415324: '1'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:36781241;b:1;}}
author:
  login: emospacemonkey
  email: stephen.emo@gmail.com
  display_name: emospacemonkey
  first_name: ''
  last_name: ''
---
Last year I spent some of my time on Oracle Cloud Certification up to OCI Professional so I have decides this year to spend my time on more practical projects. The first of which is a Spring Scheduled Routine which will post the latest NASA pic automatically to my github page via a publicly available API. Its still in progress and when it is finished I will run it on a docker image on my desktop and post about it then.

Until that time I will use this site to post some frequent tips on using Oracle Database and EBS R12 tips. I was going to cover editioned tables in Oracle EBS which increases availablity when the system is being patched but to be honest I suspect it is a brave person who relies on the feature plus editioning is a single command that I am sure Bing Co-Pilot will help with.

Instead I will mention a new feature which from a database programming point of view is a useful feature which is the Out of Place Non Atomic Materialised View. The fast refresh sounds like something you want but generally it means that data is not refreshed in one go and you will end out with users seeing no data so what you need is the original being made available while the new one is being created and this is exactly what Out of Place means.

To get this materialised view you need to run the below command

exec dbms_mview.refresh(‘TEST_MV’, out_of_place=>true, atomic_refresh=>false);
It has some restrictions for example no DBLinks and no materialised views on top of other materialised views and worst of all no outer joins so it is quite limited. Never the less I have found it useful on core materialised views, the ones at the very bottom which others are built on top of.
