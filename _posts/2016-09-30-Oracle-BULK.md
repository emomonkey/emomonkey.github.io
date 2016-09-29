---
layout: post
title: Oracle PDFMerger API does not support PDF format beyond 2004
date: 2016-09-12 22:01:49.000000000 +00:00
categories: []
tags:
- Oracle Bulk Collect ForAll Temporary Tables
- GTT
- Bulk Collect
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
I have been working on a number of concurrent requests for Oracle EBS and checking to see how I can improve the performance of some of the existing routines which do numerous updates and inserts. Not it is suggested that the updates be split up into BULK Collect and FORALL statements however this does ignore the fact that sometimes routines need to carry out calculations and checks in a certain order. It is not simply a matter of doing all the updates in one go so to keep the flow of the program I updated the routine to instead store the updates and inserts to various tables in a global temporary tables. Then this global temporary table could be processed in a step by step basis as required.

So the declaration of the global temporary table was combined with the BULK Collect and FORALL in the below manner

~~~ sql
       tmp_tb IS TABLE OF tmp_table%ROWTYPE INDEX BY BINARY_INTEGER;

       l_tmp tmp_table;

       CURSOR update_cur
       IS
       SELECT *
       FROM tmp_table
       WHERE table_name = 'A_TABLE' AND action = 'UPDATE;

       BEGIN
        OPEN update_cur;
        LOOP
        FETCH update_cur BULK COLLECT INTO l_tmp LIMIT 200;
        EXIT WHEN l_tmp.COUNT = 0;
          
             FORALL i IN l_tmp.first .. l_tmp.last
               UPDATE A_TABLE SET field1=l_tmp(i).field1 WHERE field2=l_tmp(i).field2;


        END LOOP;
        CLOSE update_cur;
       
       END

~~~

The above logic can be used and parse the changes into the database while the population of the Global Temporary Table can be done in such a way that it mirrors the flow of the original program which dotted updates and inserts behind checks and calculations. This allows us to update the program while not disturbing the flow of the program but allowing it to process it's updates and inserts efficiently.







