---
title: "Splunk Financial Dashboard"
date: 2021-04-24
tags: ["python", "tastywork", "splunk", "selenium"]
draft: false
---

## Description

Wrote python script to login to my broke, download the transactions table, parse and output to Splunk. Index data and display a dashboard with many different metrics such as "Win/loss ratio", "profit/loss avt", "biggest/smallest winner/loser", etc...

After a while I did realize the Splunk portion felt too heavy, so I feel like the dashboard could just be a single light app driven python. Maybe streamlit of sorts of app that I can quickly deploy to netlify...