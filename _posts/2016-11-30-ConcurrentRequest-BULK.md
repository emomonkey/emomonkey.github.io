---
layout: post
title: How to Wait for a Concurrent Request To Complete
date: 2016-11-30 22:01:49.000000000 +00:00
categories: []
tags:
- fnd_request.submit_request
- fnd_request.wait_for_request
- Oracle Concurrent Request
- FTP Burst
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
excerpt: !ruby/object:Hpricot::Doc
  options: {}
---
I recently put together a Concurrent Request that queried the database and used the result to create a number of folders named after the customers in the database. This concurrent routine was called from within Oracle Reports Builder in the after_report event. It needed to be called before the FTP Burst concurrent routine so I have to use the fnd_request.wait_for_request command. However it did not seem to wait for me and which had not been mentioned anywhere I checked on the web.

This thing I missed was the commit statement. It needs to be run after your submit_request and before the wait_for_request. See below 

~~~ sql
l_reqid := fnd_request.submit_request
(application =>
,program => 'XX...' -- child prg short name
,description => ''
,start_time => SYSDATE
,sub_request => TRUE
,argument1 => xx.xx1 -- child prg arguments
);

fnd_request.wait_for_request ...
  

~~~


