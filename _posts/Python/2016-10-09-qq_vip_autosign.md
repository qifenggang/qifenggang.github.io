---
layout: post
title: qq_vip_autosign
category: Python
tags: code python
keywords: selenuim python code
description: 
---

###  QQ会员自动登录签到

主要利用selenium实现

```python

#!/usr/bin/python
# -*- coding: utf-8 -*-
import re,os,time,sys
import urllib2,urllib,cookielib,socket
os.chdir(sys.path[0])
print os.getcwd()
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

try:
    print "--"*10+"start"+"--"*10
    
    browser = webdriver.Firefox()
    browser.maximize_window()
    """cap=webdriver.DesiredCapabilities.PHANTOMJS
    cap["phantomjs.page.settings.resourceTimeout"]=1000
    cap["phantomjs.page.settings.loadImages"]=False
    cap["phantomjs.page.settings.localToRemoteUrlAccessEnabled"]=True
    browser=webdriver.PhantomJS(desired_capabilities=cap)"""
    #browser=webdriver.PhantomJS()
    #browser=webdriver.PhantomJS(service_args=['--load-images=no','--disk-cache=true'])
    #browser.set_window_size(1280, 960)
    browser.implicitly_wait(10)
    browser.get("http://vip.qq.com/my/index.html")
    print browser.title
    time.sleep(5)
    browser.switch_to_frame("ui_ptlogin")
    print u'切换至浮层'
    browser.find_element_by_xpath(".//*[@id='switcher_plogin']").click()
    time.sleep(5)
    print browser.find_element_by_xpath("//*").text
    browser.find_element_by_xpath('''//input[@id='u'] ''').send_keys("139072292")
    browser.find_element_by_xpath(''' //input[@id='p']''').send_keys("")
    browser.find_element_by_xpath(''' //input[@id='login_button'] ''').click()
    time.sleep(5)
    browser.save_screenshot('1.png')
    now_handle = browser.current_window_handle
    print now_handle
    print browser.title
    WebDriverWait(browser, 10).until(lambda the_driver: the_driver.find_element_by_xpath(".//*[@id='vip_sign_entrance']/img").is_displayed())
    browser.find_element_by_xpath('''.//*[@id='vip_sign_entrance']/img''').click()
    time.sleep(3)
    browser.save_screenshot('1.png')
    #print browser.page_source
    print now_handle
    all_handles = browser.window_handles #获取所有窗口句柄
    print all_handles
    for handle in all_handles:
            if handle != now_handle:
                print handle    #输出待选择的窗口句柄
                browser.switch_to_window(handle)
                break   
    browser.find_element_by_xpath('''.//*[@id='vip_sign']/img''').click()
    print browser.title
except Exception as e :
    print 'error '
    print e
    browser.save_screenshot('erro.png')
finally:
    print u"------------------------------关闭------------------------------"
    raw_input('是否继续关闭')
    browser.close()
    browser.quit()
    
    
```
