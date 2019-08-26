---
layout: post
title: Migratory Ranks Javascript solution 
date: 2019-07-26 22:01:49.000000000 +00:00
categories: []
tags:
- JavaScript
- HackerRank
- Migratory Birds
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

In between looking at React I have been taking a look at some of the coding tasks on HackerRank mostly to help get a handle of a lot of the new functional Javascript functionality I have not used since classic ASP days. So here I make use of the sort method and the new Map object. The Map object in particular had difficulty in identifying 'undefined'. In the end I found the 'has' method and came up with the below solution.

~~~ javascript
 function migratoryBirds(arr) {

    let bMap = new Map();
    let sarr = arr.sort(function (a, b) { return a - b });
    var curval = 1;
    
    for (var i = 0; i < sarr.length; i++) {
      

        if (bMap.has(sarr[i])) {

            curval = bMap.get(sarr[i]);
            bMap.set(sarr[i], curval + 1);
        }
        else {
            
            bMap.set(sarr[i], 1);
        }
    }

    let maxval = bMap.get(sarr[0]);
    let minkey = sarr[0];

    bMap.forEach(function (value, key) {
        if (maxval < value) {
            maxval = value;
            minkey = key;
        }
    })

    /*return Array.from(bMap);*/
    return minkey
}

~~~


