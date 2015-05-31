---
layout: post
title: Using Ruby on Rails in Offline Environment 
date: 2015-05-17 22:01:49.000000000 +00:00
categories: []
tags:
- Local
- Ruby on rails
- Offline
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
I recently had the need to develop a quick ruby on rails application offline, I had all the GEMS I needed for the application and ran bundle install --local and still I got errors. It seems with the latest versions of bundler local is not offline but requires an Internet connection. 

To work offline in Ruby On Rails you need to run on bunder version 1.5.x and below. This is a bit of a gotcha for developers working in an offline environment.
