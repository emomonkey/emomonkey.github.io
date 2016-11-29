---
layout: post
title: EBS Validation in Concurrent Jobs 
date: 2016-12-01 22:01:49.000000000 +00:00
categories: []
tags:
- Oracle EBS
- validation
- Oracle Concurrent Request
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

Some more interesting tips with Oracle EBS Validation Set in R12. A Frequent Request is to Filter some of the other valuesets by Date e.g. only Purchase Orders between two date. To Do this we need to Create a From Date Value Set of type FND_STANDARD_DATE.

 

The list of Purchase Orders in the Validation Set need to be filter by this date. You would think that the value returned by FND_STANDARD_DATE would be a date but it is not. It is a character that needs formatted e.g. TO_DATE(, 'YYYY/MM/DD HH24:MI:SS'),

So in the Validation Table Information screen do the following

~~~ sql
 l_reqid := fnd_request.submit_request
_date  >=

   TO_DATE(:$FLEX$.FIN_PO_FROM_VS, 'YYYY/MM/DD HH24:MI:SS')
(application =>
,program => 'XX...' -- child prg short name
,description => ''
,start_time => SYSDATE
,sub_request => TRUE
,argument1 => xx.xx1 -- child prg arguments
);

fnd_request.wait_for_request ...
 

~~~


