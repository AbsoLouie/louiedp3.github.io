---
layout: post
title:  "Rails and the 406 error"
date:   2014-06-23 11:02:22
categories: Rails Errors
---

Today I saw my first 406 error. It was the first time I saw it and I had to do some research to understand the issue. A 406 error (per wikipedia) is thrown when the data you receive is different from what was requested. The most common occurence of the 406 error happens when JSON, specifically forgetting to convert it before sending the data.

The Rails app I was working on does not deal with JSON objects so I had to look elsewhere. After looking through the logs I noticed that the app was failing after a partial was rendered. Digging deeper I saw that the partial it was referrring to was non-existent!

This was unexpected, I didn't receive a `Missing partial layouts/_PARTIAL.erb` error. After fixing and deploying the correct code, I'm still experimenting with why I did not receive the expected error. I'll post an update if I find an answer.