---
title: "Splunk Trading Dashboard"
date: 2021-04-24
tags: ["python", "tastyworks", "splunk", "selenium"]
draft: false
---

### Description

Wrote python script to login to my broke, download the transactions table, parse and output to Splunk. Index data and display a dashboard with many different metrics such as "Win/loss ratio", "profit/loss avt", "biggest/smallest winner/loser", etc...

After a while I did realize the Splunk portion felt too heavy, so I feel like the dashboard could just be a single light app driven python. Maybe streamlit of sorts of app that I can quickly deploy to netlify...

### Code

```from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.chrome.options import Options
from selenium.common.exceptions import TimeoutException
import logging
import time
import json
import pandas as pd
import sqlite3


def get_page(url):

	driver = webdriver.Chrome()
	wait = WebDriverWait(driver, 10)
	login_path = "//*[text()='Log In']"
	signin_path = "//button[text()='Sign In']"
	transactions_path = "//"
	
	try:
		driver.get(url)
		loginelement = wait.until(EC.element_to_be_clickable((By.XPATH, login_path))).click()
		userelement = driver.find_element_by_id('username')
		userelement.send_keys('xxxxxxxxx')
		passelement = driver.find_element_by_id('password')
		passelement.send_keys('xxxxxxxxxxxxxx')
		signinelement = wait.until(EC.element_to_be_clickable((By.XPATH, signin_path))).click()
		time.sleep(3)
		driver.get('https://manage.tastyworks.com/#/accounts/transactions')
		time.sleep(1)
		table = driver.find_elements_by_tag_name("table")[0].get_attribute('outerHTML')
		df = pd.read_html(table)
		df[0].to_csv('transactions.csv', index=False)
	except Exception as e:
		print(e)
		driver.quit()
	
	

if __name__ == "__main__":
	get_page("https://tastyworks.com")```